---
type: Guide
title: Bring Your Own Virtual Agent | BYOVA over WebSocket
display_title: BYOVA over WebSocket
canonical_url: https://developer.webex.com/docs/bring-your-own-virtual-agent-over-websocket
content_type: documentation
product_group:
- webex-contact-center
categories:
- mcp
- webex-contact-center
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/bring-your-own-virtual-agent-over-websocket)

Implement a partner-hosted WebSocket virtual agent that exchanges caller audio, virtual-agent responses, and conversation events with Webex Contact Center over one secure connection per conversation.

## BYOVA over WebSocket overview

Bring Your Own Virtual Agent (BYOVA) over WebSocket provides a bidirectional, JSON-based contract between Webex Contact Center and a partner-hosted virtual-agent connector. Webex initiates and manages the WebSocket session. The partner hosts and supports the connector and owns its speech, agent, and response-generation stack.

The partner implementation can use a modular speech-to-text, agent or large language model, and text-to-speech pipeline, or a voice-native speech-to-speech model. The implementation must adapt that stack to the WebSocket media, event, turn, and lifecycle contract. A speech-to-speech model is not automatically compatible only because it accepts and produces audio.

The WebSocket contract has two endpoints:

| Endpoint | Purpose | Connection scope | Message types |
| --- | --- | --- | --- |
| `/v1/va` | Run a voice virtual-agent conversation | One connection for each `conversation_id`, reused for all turns in that conversation | `VOICE_VA_REQUEST`, `VOICE_VA_RESPONSE`, `ERROR`, `PING`, and `PONG` |
| `/v1/listVirtualAgents` | Return the virtual agents available to an organization | A separate request-response connection; the conversation connection rules do not apply | `ListVARequest` and `ListVAResponse` |

Use the published [BYOVA WebSocket AsyncAPI specifications](https://github.com/webex/dataSourceSchemas/tree/main/Services/VoiceVirtualAgent_WebSocket/a38a10b7-43e4-4676-a076-a7d6dce9387d/AsyncApiSpec) as the source of truth for JSON field names, types, required fields, and enum values. This guide describes the lifecycle and behavior that the schema alone does not explain.

## Responsibility boundary

The integration keeps the virtual-agent runtime and the Webex real-time session boundary separate.

| Partner owns | Webex owns |
| --- | --- |
| Hosting, operating, and supporting the partner connector | Initiating and managing the WebSocket session |
| Validating the WebSocket bearer token | Resolving the registered endpoint and credential |
| Speech recognition, end-of-turn detection, agent reasoning, and response generation | Sending caller media and Webex Contact Center input events |
| Text-to-speech or speech-to-speech media generation | Buffering and pacing partner audio to the caller |
| Mapping WebSocket events to partner runtime behavior | Applying turn finality and Webex session lifecycle rules |
| Emitting input-boundary, transfer, custom, and terminal events | Executing transfer and handoff in Webex Contact Center |
| Partner-side monitoring and operational support | Webex platform monitoring and support |

The partner maps the published WebSocket fields and events to its implementation. The partner does not implement or map Webex internal gRPC services or internal object models.

## Before you begin

Complete the common Service App, Bring Your Own Data Source (BYODS), Contact Center AI (CCAI), flow, and entry-point provisioning described in [Bring Your Own Virtual Agent](https://developer.webex.com/docs/bring-your-own-virtual-agent).

For the WebSocket variant, apply these WebSocket-specific values while completing that provisioning flow:

1. Implement the `/v1/va` and `/v1/listVirtualAgents` secure WebSocket endpoints before registering the data source.
2. In the Service App's **Bring Your Own Datasource Settings**, add the data source scopes and the partner-owned **Data Exchange Domain**.
3. Select WebSocket schema ID `a38a10b7-43e4-4676-a076-a7d6dce9387d` in **Data Exchange Schema**.
4. Register the partner WebSocket endpoint through the [Data Sources API](https://developer.webex.com/docs/api/v1/data-sources), using the same authorized Service App and schema.
5. Select that Service App and registered data source in the CCAI configuration used by the **Virtual Agent Voice** activity.

Do not create a second Service App for the WebSocket transport. The selected schema identifies the transport contract; there is no separate WebSocket protocol selector in the CCAI configuration.

If transcript publication is required, ask Webex support to enable it for the customer organization. Sending a transcript in the WebSocket response does not by itself enable transcript publication or persistence.

## Connection and conversation lifecycle

Webex opens one `wss` connection to `/v1/va` for one `conversation_id`. The connection can carry a welcome response followed by multiple caller and virtual-agent turns. Do not open a new connection for each turn, and do not multiplex multiple conversations on one connection.

A typical conversation follows this sequence:

1. Webex opens the secure WebSocket connection and sends the bearer token in the HTTP `Authorization` header.
2. Webex sends a `VOICE_VA_REQUEST` containing `SESSION_START` as the first application message. This message normally uses envelope sequence number `1` and contains no synthetic audio.
3. The partner can send a welcome response as one or more `PARTIAL` or `CHUNK` responses followed by one `FINAL` response.
4. Webex sends caller audio, DTMF, or input events in subsequent `VOICE_VA_REQUEST` messages.
5. The partner detects caller input boundaries and sends virtual-agent audio, transcript content when applicable, and output events in `VOICE_VA_RESPONSE` messages.
6. The partner sends exactly one `FINAL` for each logical reply. `FINAL` ends that reply, not the conversation or WebSocket connection.
7. The same connection continues with the next caller turn.
8. A transfer, application `SESSION_END`, call end, protocol failure, or transport failure ends the session. On an orderly Webex-initiated end, Webex sends one application `SESSION_END` before closing the WebSocket.

After the WebSocket connection is established, the current session is not automatically reconnected, resumed, or replayed following a connection failure. The partner must not depend on Webex replaying earlier audio, events, or turns.

## Message envelope

Messages on `/v1/va` are JSON text frames. Audio is Base64-encoded inside the JSON payload; binary WebSocket frames are not part of this contract.

The common envelope is:

```json
{
  "type": "VOICE_VA_REQUEST",
  "seq": 1,
  "ts": "2026-08-19T10:15:30Z",
  "conversation_id": "conversation-123",
  "payload": {}
}
```

| Field | Required behavior |
| --- | --- |
| `type` | Identifies the message as `VOICE_VA_REQUEST`, `VOICE_VA_RESPONSE`, `ERROR`, `PING`, or `PONG`. |
| `seq` | Positive, monotonically increasing counter owned independently by each sender for the connection. It is not a turn number or request-response correlation ID. Sequence gaps are permitted. |
| `ts` | Message creation time in RFC 3339 date-time format. |
| `conversation_id` | Stable identity of the conversation and WebSocket session. Return the same nonempty value on partner response and error envelopes. |
| `metadata` | Optional extension data. Do not use it for required authentication, media, turn, or lifecycle semantics. |
| `payload` | Request or response body for the message type. `PING`, `PONG`, and `ERROR` use their schema-defined envelope fields. |

The partner must use its own increasing sequence counter across all application responses on the connection. Do not copy the request sequence number into a `VOICE_VA_RESPONSE`. For heartbeat traffic, a `PONG` echoes the corresponding `PING` sequence number.

## Requests from Webex

Each `VOICE_VA_REQUEST` payload contains identity and configuration fields plus one input type:

```json
{
  "type": "VOICE_VA_REQUEST",
  "seq": 2,
  "ts": "2026-08-19T10:15:31Z",
  "conversation_id": "conversation-123",
  "payload": {
    "conversation_id": "conversation-123",
    "customer_org_id": "org-456",
    "virtual_agent_id": "agent-789",
    "allow_partial_responses": true,
    "vendor_specific_config": "partner-config-id",
    "voice_va_input_type": {
      "audio_input": {
        "caller_audio_b64": "<base64-encoded raw audio>",
        "encoding": "MULAW_FORMAT",
        "sample_rate_hertz": 8000,
        "language_code": "en-US"
      }
    },
    "additional_info": {
      "partner-key": "partner-value"
    }
  }
}
```

`voice_va_input_type` contains one of these objects:

| Input | Meaning |
| --- | --- |
| `audio_input` | Caller audio and its encoding, sample rate, language, and optional timestamp or single-utterance setting. |
| `dtmf_input` | Ordered DTMF digits received from the caller. |
| `event_input` | A session, interruption, no-input, or custom input event. |

Other request fields have these meanings:

| Field | Meaning |
| --- | --- |
| `customer_org_id` | Customer organization associated with the conversation. |
| `virtual_agent_id` | Selected partner virtual-agent identifier, when an agent was selected. |
| `allow_partial_responses` | Indicates whether the partner can send intermediate `PARTIAL` responses. |
| `vendor_specific_config` | Opaque partner configuration selector supplied through the integration configuration. |
| `additional_info` | Optional string-to-string context map. Treat unknown keys as optional and do not place authentication credentials or required lifecycle state in this map. |

## Responses from the partner

The partner sends virtual-agent output in `VOICE_VA_RESPONSE` messages:

```json
{
  "type": "VOICE_VA_RESPONSE",
  "seq": 8,
  "ts": "2026-08-19T10:15:32Z",
  "conversation_id": "conversation-123",
  "payload": {
    "prompts": [
      {
        "audio_content_b64": "<base64-encoded raw audio>",
        "is_barge_in_enabled": true
      }
    ],
    "output_events": [],
    "input_mode": "INPUT_VOICE_DTMF",
    "input_sensitive": false,
    "response_type": "CHUNK"
  }
}
```

| Field | Meaning |
| --- | --- |
| `prompts` | Text and inline audio to play to the caller. For streamed audio, use `audio_content_b64`. |
| `output_events` | Input-boundary, transfer, custom, no-input, no-match, or terminal events produced by the partner. |
| `input_mode` | Input accepted for the next interaction: voice, DTMF, or both. |
| `input_handling_config` | DTMF collection settings and speech timers for subsequent caller input. |
| `input_sensitive` | Marks sensitive virtual-agent output so Webex can apply secure-result handling. |
| `session_transcript` | Optional caller transcript content. Transcript publication remains customer-organization configuration dependent. |
| `session_summary` | Present in the schema, but not a supported substitute for the Webex handoff transcript. Do not depend on a partner-provided summary being persisted or displayed. |
| `disable_prompt_cancellation` | Prevents a partial automated-agent reply from being canceled by a later partner reply. It is separate from caller barge-in behavior. |
| `response_type` | `PARTIAL`, `CHUNK`, or `FINAL`. |

### Response finality

A logical virtual-agent reply can contain:

- Zero or more `PARTIAL` responses for intermediate state or transcript information.
- Zero or more `CHUNK` responses carrying streamable reply audio.
- Exactly one `FINAL` response.

The `FINAL` response can have no audio, for example when completing an event-only response. Do not send multiple `FINAL` responses for one reply. Input-boundary events such as `START_OF_INPUT`, `END_OF_INPUT`, `NO_INPUT`, and `NO_MATCH` describe recognition state and do not by themselves end the entire conversation.

## Audio format and chunking

Use the following media profile for the current Webex Contact Center integration:

| Property | Value |
| --- | --- |
| Encoding | Raw G.711 mu-law, also called PCMU or u-law |
| Sample rate | 8000 Hz |
| Channels | One, mono |
| Sample size | 8 bit, one byte per sample |
| Container | None; do not include WAV, RIFF, or other container headers |
| WebSocket encoding | Base64 inside the JSON field |
| Recommended raw chunk size | 8000-16000 bytes, representing 1-2 seconds of audio |
| Minimum raw chunk size | 320 bytes, representing 40 milliseconds of audio |
| Maximum raw chunk size | 32 KB |
| Delivery | Send each chunk as soon as it is generated; do not pace transmission to playback speed |

Webex sends caller audio in `audio_input.caller_audio_b64`. The partner returns audio in `prompts[].audio_content_b64`.

Start returning audio as soon as the first response chunk is available. Do not wait for the complete response, add leading silence, or delay each chunk according to its playback duration. Webex buffers and paces partner audio for caller playback.

The AsyncAPI schema exposes additional encoding enum values. Their presence in the schema does not establish end-to-end qualification for every codec or sample rate. Use the media profile documented in this section unless Webex has approved a different profile for the integration.

## Event contract

Event names are directional. A partner must not send an output-only event as an input event or interpret an input event as a partner output.

| Event or input | Direction | Partner behavior |
| --- | --- | --- |
| `SESSION_START` | Webex to partner | First application input on the connection. Initialize conversation state and optionally send a welcome response. |
| `audio_input` | Webex to partner | Process caller audio using the encoding and sample rate in the request. |
| `dtmf_input` | Webex to partner | Process the ordered DTMF digit list. Supported digits are 0-9, A-D, `*`, and `#`. |
| `START_OF_DTMF` | Webex to partner | Treat as an interruption associated with DTMF input. The schema does not define a separate literal `BARGE_IN` input event. |
| `NO_INPUT` | Both directions | Use direction and surrounding state to distinguish a Webex input notification from a partner recognition outcome. |
| `START_OF_INPUT` | Partner to Webex | Report that the partner detected caller speech. This event supports barge-in and input-boundary handling. |
| `END_OF_INPUT` | Partner to Webex | Report that the partner's endpointing or end-of-turn detector considers caller input complete. |
| `NO_MATCH` | Partner to Webex | Report that caller input was detected but could not be matched or understood. |
| `TRANSFER_TO_AGENT` | Partner to Webex | Request handoff from the virtual-agent leg. Include only metadata agreed for the integration. |
| `CUSTOM_EVENT` | Both directions | Map the event `name` and its parameters or metadata to an agreed partner-specific behavior. |
| `SESSION_END` | Both directions | End the application session and the virtual-agent leg. |

The partner owns speech-start and end-of-turn detection. Send the corresponding output events when the partner's speech or speech-to-speech runtime reaches those boundaries; do not wait for Webex to infer the partner's turn state.

### Barge-in

To allow the caller to interrupt a prompt, set `prompts[].is_barge_in_enabled` to `true`. When the partner detects new caller speech, send `START_OF_INPUT`. Webex uses the prompt setting and input event to stop or flush interruptible playback and continue with the caller turn.

The WebSocket schema does not contain a literal `BARGE_IN` event. Do not wait for a message with that name. DTMF interruption is represented separately through DTMF input and `START_OF_DTMF`.

### DTMF

Webex sends an ordered `dtmf_events` array in `dtmf_input`. Map each enum to the corresponding digit while preserving order. The partner can use `input_mode` and `input_handling_config.dtmf_config` in its response to control whether the next input accepts DTMF, the requested digit count, termination character, and inter-digit timeout.

### Transfer and handoff

To request transfer, send `TRANSFER_TO_AGENT` in `output_events`. The partner owns the decision to transfer and the agreed event metadata. Webex owns ending the virtual-agent leg and executing the Contact Center transfer or handoff configured for the flow.

When transcript publication is enabled, the agent handoff transcript can contain the accumulated caller and virtual-agent conversation from the virtual-agent leg. It is not a partner-generated post-call summary.

## Heartbeats, errors, and connection closure

Both sides must handle the application `PING` and `PONG` envelopes. Respond promptly to a `PING` with a `PONG` that echoes its sequence number. Heartbeat traffic maintains transport liveness; heartbeat sequence values are not turn identifiers.

The partner can send an `ERROR` envelope with a schema-defined code, numeric status, and bounded detail:

| Code | Use when |
| --- | --- |
| `unauthorized` | The bearer token or partner authorization was rejected. |
| `bad_request` | The request is invalid for the current protocol or session state. |
| `unsupported_media` | The encoding, sample rate, or media content is unsupported. |
| `upstream_error` | The partner's agent, speech, or other upstream service failed. |
| `rate_limit` | Partner capacity or quota is exhausted. |
| `timeout` | A partner operation exceeded its time limit. |

Do not include credentials, raw audio, transcripts, or other sensitive content in `detail`.

A failed WebSocket handshake, heartbeat timeout, malformed known envelope, mismatched `conversation_id`, unexpected connection close, or mid-session network failure ends the current virtual-agent session. Even when an error is classified as potentially retryable, Webex does not reconnect and replay the existing WebSocket session automatically.

## Authentication and network requirements

The production WebSocket endpoint must meet these requirements:

- Expose a publicly reachable `wss://` URL on a partner-owned domain registered in the Service App's **Data Exchange Domain**.
- Use TCP port 443 unless Webex has approved a different port for the environment.
- Present a valid TLS server certificate whose identity matches the registered hostname and whose trust chain is accepted by Webex.
- Accept a standard WebSocket upgrade and long-lived bidirectional JSON text-frame connection.
- Accept the `Authorization: Bearer <token>` header sent by Webex and validate the token according to the BYODS authentication contract.
- Configure firewalls, web application firewalls, reverse proxies, and load balancers so that they do not block WebSocket upgrades, application `PING` and `PONG`, expected message sizes, or long-lived connections.
- Scale for one concurrent WebSocket connection per active virtual-agent conversation.

Private, loopback, link-local, and plaintext `ws://` endpoints are not valid production partner targets. Do not place credentials in the URL.

Mutual TLS (mTLS) is not required for BYOVA over WebSocket. The current WebSocket contract uses server-authenticated TLS plus bearer-token validation. Optional BYOVA mTLS applies to the gRPC variant, not this WebSocket contract, and does not replace application token validation.

The AsyncAPI specification does not publish stable Webex source IP ranges. If the partner requires source-IP allowlisting, obtain the supported environment- and region-specific egress requirements from Webex support instead of allowlisting IP addresses observed during testing.

## List virtual agents

Implement `/v1/listVirtualAgents` separately from the conversation endpoint. It uses the [List Virtual Agents AsyncAPI contract](https://github.com/webex/dataSourceSchemas/blob/main/Services/VoiceVirtualAgent_WebSocket/a38a10b7-43e4-4676-a076-a7d6dce9387d/AsyncApiSpec/VoiceVirtualAgent_WsListVASchema.json).

The request contains:

- Required `customer_org_id`.
- Optional `is_default_virtual_agent_enabled`.

The response contains a `virtual_agents` array. Each entry contains a required `id` and `name` and an optional `description`. The `id` is returned as `virtual_agent_id` on a conversation request when that virtual agent is selected.

Do not wrap these messages in the `/v1/va` `VOICE_VA_REQUEST` or `VOICE_VA_RESPONSE` envelope, and do not apply the one-connection-per-`conversation_id` rule to this endpoint.

## Validate the implementation

Before production onboarding, validate these scenarios end to end:

1. Webex establishes `wss` with a valid bearer token and the partner rejects invalid authentication.
2. `SESSION_START` is the first application request and the partner can return a welcome response.
3. Caller audio is decoded as raw G.711 mu-law at 8 kHz without a WAV or RIFF header.
4. The partner streams response chunks without artificial playback pacing and sends exactly one `FINAL` per reply.
5. Multiple caller and virtual-agent turns use the same WebSocket connection.
6. Voice barge-in stops interruptible playback and produces the expected input-boundary sequence.
7. DTMF digits retain their order and the configured termination behavior works.
8. `NO_INPUT`, `NO_MATCH`, and custom events are mapped correctly.
9. `TRANSFER_TO_AGENT` ends the virtual-agent leg and follows the configured handoff path.
10. `PING` receives `PONG`, and a missing heartbeat response is observable.
11. A partner `ERROR`, malformed frame, or connection drop ends the current session without replay.
12. `SESSION_END` closes the application session cleanly.
13. When transcript publication is enabled, final transcript content reaches the intended downstream experience without exposing sensitive input.

## Frequently asked questions

### Who opens the WebSocket?

Webex opens the connection to the partner-hosted endpoint.

### Is there one WebSocket per turn?

No. There is one WebSocket for the conversation, and it carries multiple turns until the conversation ends.

### Can one WebSocket carry multiple conversations?

No. Do not multiplex conversation IDs on one connection.

### What is the first message?

A `VOICE_VA_REQUEST` containing `SESSION_START`. The partner can respond with welcome text or audio before caller audio arrives.

### What ends a virtual-agent turn?

The first valid `FINAL` for that logical partner reply. `FINAL` does not close the WebSocket or end the call.

### Who detects the end of caller speech?

The partner. Map the partner's voice activity, speech recognition, or speech-to-speech turn detector to `START_OF_INPUT` and `END_OF_INPUT` output events.

### Are barge-in, DTMF, and agent handoff supported?

Yes. Use `is_barge_in_enabled` and input-boundary events for voice interruption, `dtmf_input` for digits, and `TRANSFER_TO_AGENT` for handoff.

### Should the partner pace audio in real time?

No. Send chunks as soon as they are generated. Webex buffers and paces playback to the caller.

### Can the partner send WAV audio?

No. Send raw codec bytes without WAV, RIFF, or another container header.

### Does every codec enum in the schema work end to end?

No. Use the qualified media profile in this guide unless Webex approves a different profile for the integration.

### Can a speech-to-speech model connect without an adapter?

Only if it natively satisfies every media, event, turn, finality, and lifecycle requirement. Most implementations need a partner adapter.

### Is mTLS required?

No. WebSocket currently uses server-authenticated TLS and bearer-token validation. Optional BYOVA mTLS is gRPC-only.

### Will Webex reconnect after a network drop?

No. There is no automatic reconnect, resume, or replay for the existing conversation WebSocket.

### Is `conversation_id` a turn identifier?

No. It identifies the conversation and WebSocket session. Turn progression is carried by inputs, responses, events, and `FINAL`.

### Can the partner send binary WebSocket frames?

No. Send JSON text frames and carry audio as Base64 in the schema-defined fields.

### Are custom events supported?

Yes. Both directions support `CUSTOM_EVENT`. Agree on the event name, parameter or metadata shape, size, and ownership before relying on it.

### Are transcripts always published or stored?

No. Transcript publication is customer-organization configuration dependent. Sending `session_transcript` does not by itself guarantee persistence or display.

### Can the partner return a post-call summary?

The schema includes `session_summary`, but it is not a supported substitute for the accumulated Webex handoff transcript. Do not depend on it being persisted or displayed.

## Related documentation

- [Bring Your Own Virtual Agent](https://developer.webex.com/docs/bring-your-own-virtual-agent)
- [Bring Your Own Data Source](https://developer.webex.com/docs/bring-your-own-datasource)
- [Service Apps](https://developer.webex.com/docs/service-apps)
- [Data Sources API](https://developer.webex.com/docs/api/v1/data-sources)
- [BYOVA WebSocket AsyncAPI specifications](https://github.com/webex/dataSourceSchemas/tree/main/Services/VoiceVirtualAgent_WebSocket/a38a10b7-43e4-4676-a076-a7d6dce9387d/AsyncApiSpec)
