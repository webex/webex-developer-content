---
type: Guide
title: 'BYoVA WebSocket Connector: Expanded Implementation Guide'
display_title: 'BYoVA WebSocket Connector: Expanded Implementation Guide'
canonical_url: https://developer.webex.com/docs/byova-websocket-expanded-implementation-guide
content_type: documentation
product_group:
- webex-contact-center
categories:
- mcp
- webex-contact-center
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/byova-websocket-expanded-implementation-guide)

Build a partner-hosted WebSocket connector that exchanges caller input, virtual-agent responses, and lifecycle events with Webex Contact Center.

## Overview

This guide turns the BYoVA WebSocket contract into an implementation workflow for a partner connector. Use the existing [BYoVA over WebSocket guide](https://developer.webex.com/docs/bring-your-own-virtual-agent-over-websocket) and the published AsyncAPI schemas as the contract references for field names, enums, and required values.

## Responsibility boundary

Webex Contact Center opens and manages the conversation connection, sends caller audio and input events, and handles Contact Center actions such as transfer. The partner hosts the connector, validates the bearer token, manages conversation state, detects speech boundaries, connects to its speech or agent runtime, and returns responses and output events.

`START_OF_INPUT` and `END_OF_INPUT` are partner-to-Webex events. Send them when the partner detects the caller's speech boundaries; they are not messages to the partner's agent service.

## Establish the session

1. Expose the partner connector at a publicly reachable `wss://` endpoint with a valid TLS certificate.
2. Accept the WebSocket upgrade and validate the bearer token before processing application messages.
3. Use one connection for one `conversation_id` and keep it open across turns. Do not multiplex conversations on a connection.
4. Treat `SESSION_START` in the first `VOICE_VA_REQUEST` as the start of application state. A welcome response may follow before caller audio arrives.

The `/v1/va` endpoint carries conversation traffic. Implement `/v1/listVirtualAgents` separately for virtual-agent discovery; its request and response do not use the conversation envelope.

## Process requests

Validate the message envelope and dispatch the single input type carried by `voice_va_input_type`.

| Input | Connector behavior |
| --- | --- |
| `audio_input` | Decode the Base64 caller audio and use the media properties supplied by Webex. |
| `dtmf_input` | Process the ordered DTMF collection as one input. |
| `event_input` | Handle lifecycle or control events such as `SESSION_START`, `NO_INPUT`, and `CUSTOM_EVENT`. |

Keep conversation identity stable for the connection. Maintain the partner's own increasing sequence number for its application responses; it is not a turn number or a copy of the request sequence.

## Return responses

Send a `VOICE_VA_RESPONSE` with the next partner sequence number, the same `conversation_id`, and the output needed for the current turn. When the request sets `allow_partial_responses` to true, a logical reply can contain zero or more `PARTIAL` messages. Use `CHUNK` for streamed response audio independently, then send exactly one `FINAL`. Do not send another response for that reply after `FINAL`; it closes the reply, not the WebSocket or the call.

Use `output_events` for partner-to-Webex events, including speech boundaries and agreed Contact Center actions. Set `input_mode` to choose the next accepted caller input; use `input_handling_config` for its collection settings.

## Coordinate speech, audio, and DTMF

The partner owns speech-start and end-of-turn detection. Send `START_OF_INPUT` when caller speech begins and `END_OF_INPUT` when the partner's endpointing logic considers the input complete. Configure barge-in on the prompt when callers should be able to interrupt playback.

Set `input_mode` to accept DTMF on the next input. Use `input_handling_config.dtmf_config` to configure collection length, terminator, and inter-digit timeout. Webex sends the digits as one ordered collection. For media formats, response streaming, barge-in timing, and DTMF flows, see the existing BYoVA over WebSocket guide.

## Handle errors and close the session

Return only schema-defined error codes and bounded details. Do not put bearer tokens, raw audio, transcripts, or other sensitive content in error details. Avoid tight retry loops for rate limits. Webex does not reconnect and replay an established conversation after a connection failure.

Release conversation state and close the session on `SESSION_END`, transfer, protocol error, or transport failure. Respond promptly to `PING` with `PONG` using the same sequence number.

## Validate the connector

- Confirm the authenticated `wss://` handshake and first `SESSION_START` request.
- Confirm one connection carries multiple turns for one conversation.
- Confirm audio, DTMF, and event inputs dispatch to the correct partner behavior.
- Confirm speech-boundary events, output sequencing, and one `FINAL` per reply.
- Confirm `PING` receives a matching `PONG` and exit events release state.

## References

- [BYoVA over WebSocket](https://developer.webex.com/docs/bring-your-own-virtual-agent-over-websocket)
- [Published BYoVA WebSocket AsyncAPI schemas](https://github.com/webex/dataSourceSchemas/tree/main/Services/VoiceVirtualAgent_WebSocket/a38a10b7-43e4-4676-a076-a7d6dce9387d/AsyncApiSpec)
- [Java WebSocket JSON sample](https://github.com/CiscoDevNet/webex-contact-center-provider-sample-code/tree/main/bring-your-own/virtual-agent/web-socket-interface/simulators/byova-websocket-json-java)
