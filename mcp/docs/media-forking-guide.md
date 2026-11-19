---
type: Guide
title: Media Forking | Guide
display_title: Guide
canonical_url: https://developer.webex.com/docs/media-forking-guide
content_type: documentation
product_group:
- webex-contact-center
categories:
- mcp
- webex-contact-center
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/media-forking-guide)

Implement, register, configure, and verify a partner-hosted Media Forking gRPC endpoint that receives caller and agent audio from Webex Contact Center.

## Before you begin

The customer organization must have the Media Forking offer (`MFCS`) on its Webex Contact Center subscription. The orderable SKUs are `A-FLEX-MEDSTRM` (Flex 3) and `E3CE-MEDSTRM` (Enterprise Agreement). For Flex 3 ordering details, see the [ordering guide](https://www.cisco.com/c/en/us/products/collateral/customer-collaboration/collab-flex-3-contact-center-og.html) and [data sheet](https://www.cisco.com/c/en/us/products/collateral/customer-collaboration/collab-flex-3-contact-center-ds.html).

Prepare a Webex Contact Center organization with a Full Admin who can authorize a Service App and an administrator who can edit, validate, and publish a flow. Implement a publicly reachable gRPC endpoint and secure it with TLS using a currently valid, publicly issued server certificate for the registered hostname. Optionally, add [mutual TLS (mTLS)](https://github.com/CiscoDevNet/webex-contact-center-provider-sample-code/blob/main/mtls-authentication.md) for transport-level client authentication. Require a client certificate and validate its issuer, validity window, and tenant-documented Webex CCAI identity. Do not use mTLS instead of runtime JSON Web Signature (JWS) validation.

Use the [CiscoDevNet provider sample](https://github.com/CiscoDevNet/webex-contact-center-provider-sample-code/tree/main/media-forking) as a protocol reference, and adapt it to your processing and operational requirements. Its current Java validator retrieves keys before checking the issuer allowlist and tests every returned key; do not reuse that authentication path unchanged.

## Try the receiver sample

The [WebexSamples Node.js receiver](https://github.com/WebexSamples/webex-contact-center-media-forking-sample) provides TLS and JWS validation, the media and health RPCs, bounded audio handling, and optional WAV recording. Start with its synthetic demo before connecting an organization.

Install Node.js 24, then run:

```sh
git clone https://github.com/WebexSamples/webex-contact-center-media-forking-sample.git
cd webex-contact-center-media-forking-sample
npm ci
npm run demo
```

Expect `media_received` logs for `CALLER` and `AGENT`, `stream_completed`, and `Demo passed`. The demo sends distinct one-second synthetic tones over loopback, verifies a final `SUCCESS`, and checks that an unauthenticated stream is rejected. It needs no Webex organization or credentials. Its temporary keys and plaintext loopback transport are confined to the demo; `npm start` requires TLS and Webex JWS validation.

For a real organization, follow the [sample setup walkthrough](https://github.com/WebexSamples/webex-contact-center-media-forking-sample/blob/main/docs/SETUP.md) and the registration and flow steps below. Copy `.env.example` to `.env`, set the registered data-source bindings and TLS certificate/key paths, and run `npm start`. The receiver requires TLS 1.3 and an HTTP/2-capable public network path. Keep credentials and tenant configuration out of source control.

Add your processing in [`lib/audio.mjs`](https://github.com/WebexSamples/webex-contact-center-media-forking-sample/blob/main/lib/audio.mjs). The handler receives validated, normalized non-empty audio and an `AbortSignal`; honor cancellation and set downstream timeouts. The starter accepts one configured customer organization and data source per process. Its [validation notes](https://github.com/WebexSamples/webex-contact-center-media-forking-sample/blob/main/docs/VALIDATION.md) distinguish synthetic checks, live SDK calls, and remaining coverage; the sample is not certified for production capacity or reliability.

## Implement the gRPC endpoint

Webex Contact Center acts as the gRPC client. Your partner-hosted service acts as the server and implements this bidirectional streaming RPC:

```protobuf
service ConversationAudio {
  rpc StreamConversationAudio(stream ConversationAudioForkingRequest)
      returns (stream ConversationAudioForkingResponse);
}
```

Handle opening metadata and audio packets separately:

1. Validate the opening message's `conversation_id`, `customer_org_id`, `audio.role`, and `audio.role_id`, and retain the declared encoding and sample rate for that leg. Webex can send this metadata before any audio bytes arrive.
2. Process non-empty `audio.audio_data` as raw audio. Later packets can omit `customer_org_id`, encoding, and sample rate; use only the previously validated metadata for the same conversation and leg. Reject explicit identity mismatches. Preserve `audio.audio_timestamp` when present; do not invent a capture timestamp when it is omitted.
3. Read `audio.role` and `audio.role_id` to identify the media leg.
4. Use `(customer_org_id, conversation_id, role, role_id)` as the processing key so that individual media legs remain separate.
5. Treat re-established streams as separate RPCs. Design downstream idempotency for your consumer; conversation and leg identifiers group media but are not unique packet identifiers. Capture timestamps are not a documented packet sequence.
6. Use `ConversationAudioForkingResponse.status_message` and `error_code` for application status and processing errors. Terminate the RPC with an appropriate gRPC status for authentication, transport, or unrecoverable stream failures.
7. Complete the response stream after Webex completes its request stream and your endpoint finishes processing.

![Caller and agent media use independent RPCs to the same receiver. Each validates its JWS, processes audio, drains queued work after client half-close, and returns one final SUCCESS.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt6665993063c98692/6aee373f421b33e40acc9531/media-stream-lifecycle-dual-rpc.jpg)

*Example caller and agent RPCs to the same receiver. Timing is illustrative; each RPC completes independently and can share a TLS connection.*

Caller and agent media can arrive on separate RPCs. Media Forking sends variable-sized raw mono audio frames, not a WAV container, at 8 kHz or 16 kHz. The protobuf defines `LINEAR16`, `MULAW`, and `ALAW`. The canonical Java sample logs the encoding and can append raw audio bytes to files; it does not decode or transcode them. Decode or transcode the audio as required by your downstream processor. The samples send one final `SUCCESS` acknowledgment per RPC after Webex completes its request stream, so do not expect a response for every audio frame.

Implement `Check` on the separate `com.cisco.wcc.ccai.v1.Health` service defined in the sample's [health contract](https://github.com/CiscoDevNet/webex-contact-center-provider-sample-code/blob/main/media-forking/simulators/media-forking-java/src/main/proto/com/cisco/wcc/ccai/v1/health.proto). Call the gRPC `Check` method on the service endpoint. This contract does not define an HTTP GET health page at `/v1/ping`. Return `SERVING` while the media service is ready to receive streams and `NOT_SERVING` when it is not ready.

> **Important:** The customer is responsible for keeping the receiving service healthy and able to receive and process streamed data. Webex Contact Center does not maintain back pressure. Keep the gRPC receive callback non-blocking; buffer briefly within fixed bounds or shed load explicitly. If the receiver cannot receive or process the stream, any resulting data loss is permanent and cannot be recovered.

## Create and authorize a Service App

1. Create a [Service App](https://developer.webex.com/admin/docs/service-apps) in Webex for Developers.
2. Request the `spark-admin:datasource_read` and `spark-admin:datasource_write` scopes to show the data-source settings.

   ![Active spark-admin:datasource_read and spark-admin:datasource_write scope choices before selection in the new Service App form.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt74da9bd4945585b9/6aee32f5bf422f9af6f1c272/data-source-scopes-active.jpg)

   *Data-source scope choices before selection in the new Service App form.*
3. Enter a data exchange domain owned by the Service App owner that contains the gRPC endpoint. Do not include a port.
4. Select the Media Forking schema shown when you set up the Service App.

   ![New Service App form with the active audio_forking_schema option selected.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt5f8ab72fa35db464/6aee32848923da4cbd4ab510/media-forking-schema-active.jpg)

   *Example: `audio_forking_schema` selected in a new Service App form.*
5. Make the Service App visible to the target organization. Request admin authorization for the developer's own organization; for a non-affiliated customer organization, submit the app to Webex App Hub for review.
6. Ask a Full Admin of the customer organization to review and authorize the Service App in Control Hub.

   ![Control Hub displays the Media Forking Dev Sample app with Authorized enabled.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt892353e71f033239/6aee21da38745e032c661e6f/service-app-authorized.jpg)

   *Example of a Service App already authorized in Control Hub.*
7. Obtain the organization-specific Service App access and refresh tokens.
8. Store the app credentials and tokens securely.

Do not use a schema identifier copied from another integration. Use the Media Forking schema selected when you set up this integration.

## Register the data source

Use the [Data Sources API](https://developer.webex.com/docs/api/v1/data-sources) with the organization-specific Service App access token.

1. Register the endpoint for the customer organization.
2. Follow the current API request schema. In `schemaId`, supply the Media Forking schema selected for the Service App; also supply the endpoint URL, audience, subject, nonce, and a supported token lifetime.
3. Confirm that the endpoint URL satisfies the Service App's data exchange domain rule.
4. Record the returned data source identifier.
5. Before the current JWS token expires, update the registered data source with the complete required payload, including its current `status` and a new `nonce`. The configured token lifetime can be at most 1440 minutes (24 hours). Renew with a safety margin before the signed JWT `exp`; do not wait until the last second shown by a REST expiry display. OAuth access-token renewal and data-source JWS renewal are separate operations; the sample does not automate them.

Use OAuth tokens only to manage the data source through the API. For each media RPC, extract the JWS from the gRPC `authorization` metadata and validate all of the following:

- The issuer against an allowlist of Webex issuers before retrieving verification keys.
- The `RS256` algorithm and RSA signature, using the Cisco public key identified by the JWS header's `kid` from `${iss}/oauth2/v2/keys/verificationjwk/`.
- The expiration time.
- The audience and subject claims against the values registered for the data source, and the presence of the JWT ID.
- The `com.cisco.datasource.url` claim against the registered endpoint URL.
- The `com.cisco.datasource.schema.uuid` claim against the selected Media Forking schema.
- The signed `com.cisco.org.uuid` claim against the opening metadata's `customer_org_id`. Keep that binding for later packets that omit the field, and reject an explicit mismatch.

Reject a missing or invalid JWS with `UNAUTHENTICATED`. Keep JWS validation enabled even when you use mTLS.

<a id="create-the-media-forking-configuration"></a>

## Select the Service App

Select the authorized Service App directly in the **Start Media Stream** activity. Media Forking does not require a separate configuration under **Contact Center > Integrations > Features**.

![Start Media Stream activity settings show Media Forking Dev Sample (Service App) as the Media destination.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltcbbaf07f0d10d428/6aee21bdc7335a8917274ec6/service-app-media-destination.jpg)

*Example media destination; select the Service App authorized for your organization.*

## Configure the flow

1. Enable the test agent for Contact Center, assign its site, team, and desktop profile, and ensure the queue distributes calls to that team.
2. Open the target inbound flow in Flow Designer. Route the main flow through **Queue Contact** to the intended queue.
3. In **Event Flows**, connect **AgentAccepted** (called **AgentAnswered** in older flows) to **Start Media Stream**.
4. Under **Media streaming settings > Media destination**, select the authorized **Service App** directly.
5. Connect the activity's success and failure exits to **End Flow** so the event handler finishes.

   ![AgentAccepted connects to Start Media Stream, whose normal and failure paths both connect to End Flow.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltd69fae50b7ceffa1/6aee21da421b3369aecc9439/agent-accepted-media-stream.jpg)

   *Example from a saved flow version. Generated activity labels can differ in your flow.*
6. Validate the flow, resolve validation errors, and publish it.
7. Map the test entry point to that flow and its published version label.

The activity needs an answered caller-agent conversation. A normal main path usually runs before the agent connects and can fail with `callNotAnswered`; use the agent-answer event handler for the inbound path above.

For queue-specific conditional logic in Flow Designer, see [Enabling media streaming for specific queues](https://help.webex.com/en-us/article/n5jhgdi/Enabling-media-streaming-for-specific-queues) in the Webex Help Center.

## Verify the integration

1. Confirm that the health `Check` RPC reports `SERVING` when the receiver is ready and `NOT_SERVING` when it is not ready.
2. Confirm that the endpoint rejects an audio RPC that does not contain a valid JWS.
3. Place a test call through the configured flow.
4. Have an agent answer the call.
5. Confirm that the **Start Media Stream** activity opens a stream to the registered endpoint.
6. Confirm receipt of non-empty audio for both `CALLER` and `AGENT` roles, including when they use separate RPCs.
7. Verify that the endpoint preserves conversation and role identifiers.
8. Verify that the endpoint handles opening metadata, sparse audio packets, and the declared encoding and sample rate. Record whether capture timestamps are supplied.
9. End the call and confirm that both sides close the stream cleanly.
10. Check server logs for expired tokens, URL or schema claim mismatches, stream failures, and successful completion.

## Record WAV audio with the sample

Media Forking supplies raw audio; the Node.js sample can wrap received bytes in a WAV container without transcoding. Recording is disabled by default. To try it with synthetic caller and agent tones:

```sh
RECORDING_DIR=./recordings npm run demo
```

![The optional recorder wraps raw audio in separate caller and agent WAV files, writes partial files, then finalizes the header, syncs, closes and renames each file.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt5f50f2625ddea0f5/6aee21e56c10e6d96b818394/wav-recording-output.jpg)

*Caller and agent labels illustrate separate outputs. Actual filenames include generated stream, leg, and segment identifiers.*

To record real incoming streams, set `RECORDING_DIR=./recordings` in `.env` and run `npm start`. Each RPC/participant leg gets a separate mono WAV file using its declared `LINEAR16`, `MULAW`, or `ALAW` encoding at 8000 or 16000 Hz. Use a player that supports the codec. Reconnects create new files; format changes start new segments. Files retain arrival order without mixing participants, filling gaps, or aligning timestamps.

Look for `recording_saved` followed by `stream_completed`. The writer finalizes the header, syncs and closes the file, then renames `.wav.partial` to `.wav` before acknowledging success. Cancellation can still produce a valid WAV covering only part of a call; check `stream_failed` as well. A crash or disk error can leave `.partial` files, which the sample does not recover automatically.

The sample requires a private, writable recording directory (`0700`) and creates files with mode `0600`. Keep recordings outside web-served paths, use encrypted storage, monitor available space, and define a retention/cleanup policy. Disk exhaustion fails the stream. See [recording behavior and limits](https://github.com/WebexSamples/webex-contact-center-media-forking-sample#record-wav-audio) before enabling capture.

## Troubleshoot the connection

| Symptom | Check |
| --- | --- |
| Service App is unavailable or cannot be authorized | Confirm the Media Forking subscription, selected schema, app visibility, and customer admin authorization. A data-source registration alone does not establish entitlement. |
| No configuration appears under Integrations > Features | Select the Service App directly in **Start Media Stream**; the flow does not need a separate Features configuration. |
| `callNotAnswered` | Start streaming after the agent answers, using the agent-answer event handler described above. |
| No connection or unhealthy receiver | Check the registered hostname and URL, publicly trusted TLS certificate, HTTP/2 routing, and Cisco gRPC health `Check`. An HTTP health page does not implement that contract. |
| `UNAUTHENTICATED` | Check signed expiry and the registered issuer, audience, subject, URL, schema, and organization bindings. Renew an expired data-source JWS with a fresh nonce and the complete update payload. Keep token values out of logs. |
| Audio arrives without metadata fields or timestamps | Retain validated opening metadata for that leg and preserve missing timestamps as absent. Do not reject a packet only because inherited fields are omitted. |
| Recording fails or only a `.partial` file exists | Check directory permissions, write/search access, disk space, and stream failure logs. A finalized WAV can still contain only part of a call. |
