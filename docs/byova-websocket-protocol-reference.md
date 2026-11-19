---
type: Guide
title: 'BYoVA WebSocket: Protocol Reference'
display_title: 'BYoVA WebSocket: Protocol Reference'
canonical_url: https://developer.webex.com/docs/byova-websocket-protocol-reference
content_type: documentation
product_group:
- webex-contact-center
categories:
- mcp
- webex-contact-center
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/byova-websocket-protocol-reference)

Use this reference to identify BYoVA WebSocket endpoints, message envelopes, input types, response types, event directions, and error handling.

## Overview

The [BYoVA over WebSocket guide](https://developer.webex.com/docs/bring-your-own-virtual-agent-over-websocket) explains the full lifecycle and partner implementation. The published AsyncAPI schemas are authoritative for field types, required fields, and enum values.

## Endpoints

| Endpoint | Purpose |
| --- | --- |
| `/v1/va` | Bidirectional conversation traffic, including requests, responses, heartbeat messages, and errors. |
| `/v1/listVirtualAgents` | Separate discovery operation that returns virtual agents available to an organization. |

Use one secure WebSocket connection for one `conversation_id`. Keep it open across turns and do not multiplex conversations on the same connection. Virtual-agent discovery is a separate request-response operation and does not use the conversation envelope.

## Conversation message envelope

A conversation message is a JSON text frame. The common envelope contains:

| Field | Meaning |
| --- | --- |
| `type` | Message kind, such as `VOICE_VA_REQUEST`, `VOICE_VA_RESPONSE`, `PING`, `PONG`, or `ERROR`. |
| `seq` | Sender-owned sequence number. It is not a turn number or request-response correlation ID. |
| `ts` | RFC 3339 message timestamp. |
| `conversation_id` | Stable conversation identity for the WebSocket session. |
| `payload` | Request or response body for voice messages. Heartbeat and error messages use their schema-defined top-level fields. |

Example `SESSION_START` request with the required payload fields:

```json
{
  "type": "VOICE_VA_REQUEST",
  "seq": 1,
  "ts": "2026-08-19T10:15:31Z",
  "conversation_id": "conversation-123",
  "payload": {
    "conversation_id": "conversation-123",
    "customer_org_id": "org-123",
    "voice_va_input_type": {
      "event_input": {
        "event_type": "SESSION_START"
      }
    }
  }
}
```

Each sender maintains an independent increasing sequence counter for application messages. A `PONG` echoes the `seq` from the corresponding `PING`.

## Inputs from Webex

`VOICE_VA_REQUEST.payload.voice_va_input_type` contains one input object:

| Input | Meaning |
| --- | --- |
| `audio_input` | Caller audio and media properties. Audio is Base64-encoded in JSON. |
| `dtmf_input` | An ordered collection of DTMF events. |
| `event_input` | A lifecycle or control event, such as `SESSION_START`, `NO_INPUT`, or `CUSTOM_EVENT`. |

`SESSION_START` is the first application input on a conversation connection. Other event examples include `SESSION_END`, `START_OF_DTMF`, and `CUSTOM_EVENT`.

## Responses from the partner

`VOICE_VA_RESPONSE.payload` can contain prompts, output events, input mode, input-handling configuration, and a response type.

| Response type | Use |
| --- | --- |
| `PARTIAL` | Intermediate response content; send only when `VOICE_VA_REQUEST.payload.allow_partial_responses` is `true`. |
| `CHUNK` | Streamed response audio. |
| `FINAL` | Closes one logical reply. Send exactly one for each reply. |

A `FINAL` does not close the WebSocket or end the call. It may be audio-less. Do not send more output for that logical reply after `FINAL`.

## Event directions

| Direction | Event examples |
| --- | --- |
| Webex to partner | `SESSION_START`, `SESSION_END`, `NO_INPUT`, `START_OF_DTMF`, `CUSTOM_EVENT` |
| Partner to Webex | `START_OF_INPUT`, `END_OF_INPUT`, `NO_MATCH`, `NO_INPUT`, `CUSTOM_EVENT`, `TRANSFER_TO_AGENT`, `SESSION_END` |

`START_OF_INPUT` and `END_OF_INPUT` are partner-to-Webex input-boundary events. The partner sends them based on its speech detection and end-of-turn logic. `SESSION_END` can be sent in either direction to end the application session.

## Authentication, heartbeat, and errors

Validate the bearer token during the WebSocket upgrade before processing application messages. Respond promptly to `PING` with `PONG` and the matching sequence number.

Partner error envelopes use schema-defined codes, including `unauthorized`, `bad_request`, `unsupported_media`, `upstream_error`, `rate_limit`, and `timeout`. Keep error details bounded and do not include credentials, raw audio, transcripts, or other sensitive content.

## References

- [BYoVA over WebSocket](https://developer.webex.com/docs/bring-your-own-virtual-agent-over-websocket)
- [Published BYoVA WebSocket AsyncAPI schemas](https://github.com/webex/dataSourceSchemas/tree/main/Services/VoiceVirtualAgent_WebSocket/a38a10b7-43e4-4676-a076-a7d6dce9387d/AsyncApiSpec)
- [Java WebSocket JSON sample](https://github.com/CiscoDevNet/webex-contact-center-provider-sample-code/tree/main/bring-your-own/virtual-agent/web-socket-interface/simulators/byova-websocket-json-java)
