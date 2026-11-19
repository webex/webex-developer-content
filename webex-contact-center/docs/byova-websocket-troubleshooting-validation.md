---
type: Guide
title: 'BYoVA WebSocket: Troubleshooting and Validation'
display_title: 'BYoVA WebSocket: Troubleshooting and Validation'
canonical_url: https://developer.webex.com/docs/byova-websocket-troubleshooting-validation
content_type: documentation
product_group:
- webex-contact-center
categories:
- mcp
- webex-contact-center
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/byova-websocket-troubleshooting-validation)

Use these checks to validate a partner BYoVA WebSocket connector and isolate connection, media, turn-taking, DTMF, and cleanup failures.

## Overview

For field names, required values, and the complete conversation lifecycle, see the [BYoVA over WebSocket guide](https://developer.webex.com/docs/bring-your-own-virtual-agent-over-websocket) and its published AsyncAPI schemas.

## Connection and authentication

| Symptom | Checks |
| --- | --- |
| WebSocket handshake is rejected | Confirm the endpoint is reachable over `wss://`, the certificate is valid for its hostname, and the bearer token is present and accepted. |
| The first message is rejected | Confirm `SESSION_START` is the first application input and that the request uses the expected JSON envelope. |
| Messages are associated with the wrong call | Keep one connection per `conversation_id` and return the same conversation ID in partner responses and errors. |
| Heartbeat fails | Respond promptly to `PING` with `PONG` using the same sequence number. |

## Audio and response sequencing

| Symptom | Checks |
| --- | --- |
| Audio is rejected or sounds wrong | Confirm raw G.711 mu-law/PCMU, 8 kHz, mono audio. Keep the payload Base64-encoded inside JSON and do not add a WAV or RIFF header. |
| Response starts late or sounds choppy | Send each audio fragment as soon as it is generated; do not pace transmission to playback duration. Check the 320-byte minimum and 32 KB maximum. |
| Streamed audio is malformed | Confirm chunk audio contains raw, headerless media bytes and the response follows the published AsyncAPI schema. |
| A reply never completes or repeats | Send `PARTIAL` only when the request sets `allow_partial_responses` to true; use `CHUNK` for streamed audio independently. Then send exactly one `FINAL` and no more output for that reply. |

## Voice and barge-in

- Send `START_OF_INPUT` when the partner detects caller speech and `END_OF_INPUT` when its endpointing logic considers the speech complete.
- Without barge-in, expect the next caller-audio stream after `FINAL`; speech spoken while the prompt plays is not delivered to the partner.
- For caller interruption, enable `prompts[].is_barge_in_enabled` and report detected speech with `START_OF_INPUT`.
- Do not wait for a literal `BARGE_IN` event; the WebSocket contract uses the prompt setting and input-boundary events.

## DTMF

- Process `dtmf_input` as one ordered collection, not one request per key press.
- Confirm `input_mode` accepts DTMF and `input_handling_config.dtmf_config` sets the intended length, terminator, and inter-digit timeout.
- Check that collection ends on the configured terminator, maximum length, or inter-digit timeout.
- Use `START_OF_DTMF` as the Webex-to-partner DTMF event; do not treat it as a partner output event.

## Errors and session cleanup

Handle schema-defined errors such as `unauthorized`, `bad_request`, `unsupported_media`, `upstream_error`, `rate_limit`, and `timeout`. Avoid tight retry loops for rate limits and do not replay an already-started conversation unless the platform contract explicitly supports it.

On `SESSION_END`, transfer, protocol error, or transport failure, release conversation state and close the session. Keep bearer tokens, raw audio, transcripts, and other sensitive content out of error details and routine diagnostic logs.

## End-to-end checklist

- [ ] The authenticated secure WebSocket handshake succeeds.
- [ ] `SESSION_START` initializes one conversation on one connection.
- [ ] Caller audio is decoded with the encoding and sample rate supplied by Webex.
- [ ] Speech boundaries are reported to Webex.
- [ ] Audio fragments follow the current media profile and are sent without artificial pacing.
- [ ] For the next caller input, `input_mode` is correct and `input_handling_config` supplies any needed DTMF collection settings or speech timers.
- [ ] Exactly one `FINAL` closes each logical reply.
- [ ] Barge-in and non-barge-in timing match the configured prompt behavior.
- [ ] DTMF digits are collected and processed in order.
- [ ] `PING` receives a matching `PONG`.
- [ ] Exit events release state and close the session.

## References

- [BYoVA over WebSocket](https://developer.webex.com/docs/bring-your-own-virtual-agent-over-websocket)
- [Published BYoVA WebSocket AsyncAPI schemas](https://github.com/webex/dataSourceSchemas/tree/main/Services/VoiceVirtualAgent_WebSocket/a38a10b7-43e4-4676-a076-a7d6dce9387d/AsyncApiSpec)
- [Java WebSocket JSON sample](https://github.com/CiscoDevNet/webex-contact-center-provider-sample-code/tree/main/bring-your-own/virtual-agent/web-socket-interface/simulators/byova-websocket-json-java)
