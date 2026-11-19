---
type: Guide
title: Bring Your Own Virtual Agent | BYOVA over gRPC
display_title: BYOVA over gRPC
canonical_url: https://developer.webex.com/docs/bring-your-own-virtual-agent-over-grpc
content_type: documentation
product_group:
- webex-contact-center
categories:
- mcp
- webex-contact-center
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/bring-your-own-virtual-agent-over-grpc)

Implement a partner-hosted gRPC virtual agent that exchanges caller audio, virtual-agent responses, and conversation events with Webex Contact Center.

## BYOVA over gRPC overview

Bring Your Own Virtual Agent (BYOVA) over gRPC uses the published `VoiceVirtualAgent` protobuf contract. Webex Contact Center is the gRPC client, and your connector hosts the gRPC server and adapts your speech and AI services to the Webex media and event model.

The service exposes two RPCs:

| RPC | Purpose |
| --- | --- |
| `ProcessCallerInput` | Bidirectional stream for caller audio, DTMF, input events, prompts, and output events. |
| `ListVirtualAgents` | Unary request that returns the virtual agents available to an organization. |

Use the published [Voice Virtual Agent protobuf definitions](https://github.com/webex/dataSourceSchemas/tree/main/Services/VoiceVirtualAgent_5397013b-7920-4ffc-807c-e8a3e0a18f43/Proto) as the source of truth for message fields and enum values. The [CiscoDevNet gRPC connector samples](https://github.com/CiscoDevNet/webex-contact-center-provider-sample-code/tree/main/bring-your-own/virtual-agent/grpc-interface) provide Java and Python reference implementations.

## Before you begin

Complete the common Service App, Bring Your Own Data Source (BYODS), Contact Center AI (CCAI), flow, and entry-point provisioning described in [Bring Your Own Virtual Agent](https://developer.webex.com/docs/bring-your-own-virtual-agent).

For the gRPC variant:

1. Implement a publicly reachable TLS-enabled gRPC server before registering the data source.
2. Select Voice Virtual Agent schema ID `5397013b-7920-4ffc-807c-e8a3e0a18f43` for the Service App and data source.
3. Register the gRPC endpoint through the [Data Sources API](https://developer.webex.com/docs/api/v1/data-sources).
4. Select the Service App and data source in the CCAI configuration used by the **Virtual Agent Voice** activity.

## Conversation and RPC lifecycle

The `conversation_id` remains the same for the entire virtual-agent leg, but the gRPC stream does not. Webex opens a new `ProcessCallerInput` bidirectional RPC for each logical interaction, such as session start, caller audio, or DTMF input.

A typical conversation follows this sequence:

1. Webex starts an RPC and sends a `VoiceVARequest` containing the `SESSION_START` event. The first request does not contain synthetic audio.
2. Your connector starts the corresponding session with its virtual agent and returns the welcome prompt.
3. Webex finishes sending requests for that RPC and half-closes its side of the stream.
4. After sending every response for that interaction, your connector completes its side of the RPC.
5. Webex opens another RPC for the next caller input while reusing the same `conversation_id`.
6. When the caller hangs up, Webex sends `SESSION_END`. A connector can instead return `TRANSFER_TO_AGENT`, `SESSION_END`, or a configured `CUSTOM_EVENT` to leave the virtual-agent flow.

Complete every RPC normally after its responses are sent. Use gRPC error status only for unexpected failures; do not leave a completed interaction open while waiting for the next turn.

## Handle caller input

Each `VoiceVARequest` contains exactly one of these inputs:

| Input | Connector behavior |
| --- | --- |
| `audio_input` | Consume the caller audio stream, detect speech and silence, and send `START_OF_INPUT` and `END_OF_INPUT` at the correct boundaries. |
| `dtmf_input` | Process the ordered DTMF digits and return the next prompt, transfer, or session event. |
| `event_input` | Handle lifecycle events such as `SESSION_START`, `SESSION_END`, `NO_INPUT`, `START_OF_DTMF`, and `CUSTOM_EVENT`. |

The reference connectors process G.711 mu-law caller audio at 8 kHz. Read the encoding and sample rate from each request instead of assuming that all future inputs use the sample defaults.

Send `END_OF_INPUT` only after detecting the end of the caller's utterance. It tells Webex to stop streaming caller audio for that interaction.

## Stream virtual-agent audio

Choose one response mode at the start of the call and keep it for the conversation:

| Mode | Use when | Required completion |
| --- | --- | --- |
| Whole WAV | The complete prompt is already available. | Send one `FINAL` response containing audio with its WAV header, then complete the RPC. |
| Chunked audio | Audio becomes available progressively, such as output from a generative or speech-to-speech model. | Send headerless audio in one or more `CHUNK` responses, then an empty-audio `FINAL`, and complete the RPC. |

For chunked responses, the reference contract allows 100 bytes through 64 KB per chunk. Send chunks as they become available without adding artificial silence; Webex buffers and paces the audio for caller playback.

Each prompt also sets `is_barge_in_enabled`:

- When enabled, caller speech or DTMF can interrupt playback. Webex drops prompts that have not played, and a new input RPC carries the caller input. Stop producing obsolete audio for the interrupted reply when your virtual-agent runtime supports cancellation.
- When disabled, Webex finishes the prompt and caller input received during playback can be dropped.

`disable_prompt_cancellation` controls whether a later partner response can cancel an earlier partial response. It does not disable caller barge-in.

## Authenticate every RPC

Validate the JWS/JWT from the gRPC `authorization` metadata on every call. At minimum, verify the signature, expiration, issuer, required claims, and that the data source URL and schema claims match the registered connector.

The Java sample includes a complete JWT validation pattern. The Python sample contains an authentication scaffold and must be hardened before production use. Never disable token validation on a publicly reachable endpoint.

For transport-level client authentication in addition to JWS/JWT, see [mTLS Authentication](https://developer.webex.com/docs/bring-your-own-virtual-agent-mtls-authentication).

## Run a reference connector

Clone the [provider sample code](https://github.com/CiscoDevNet/webex-contact-center-provider-sample-code), then choose either implementation.

For Java 21 or later:

```bash
cd bring-your-own/virtual-agent/grpc-interface/simulators/byova-grpc-java
./mvnw spring-boot:run
```

For Python 3.10 or later:

```bash
cd bring-your-own/virtual-agent/grpc-interface/simulators/byova-grpc-python
chmod +x run.sh
./run.sh
```

Both samples listen on port `8086` by default. They use local prompts and simple event handling for smoke testing; replace that behavior with your production virtual-agent integration.

## Adapt and verify the connector

Before onboarding a customer:

1. Return your real agent catalog from `ListVirtualAgents`.
2. Map audio, DTMF, and input events to your virtual-agent runtime.
3. Stream prompts and output events using the required response finality.
4. Verify `SESSION_START`, multi-turn audio, DTMF, barge-in, transfer, custom event, caller hang-up, and connector error scenarios.
5. Confirm JWT rejection and, when enabled, mTLS rejection before testing valid credentials.
6. Add production monitoring, timeouts, capacity limits, and graceful shutdown behavior around the sample implementation.

The sample connector demonstrates the protocol; the partner remains responsible for hosting, scaling, securing, and supporting the production service.
