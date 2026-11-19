---
type: Guide
title: 'BYoVA WebSocket: Audio, DTMF, and Barge-in Flows'
display_title: 'BYoVA WebSocket: Audio, DTMF, and Barge-in Flows'
canonical_url: https://developer.webex.com/docs/byova-websocket-audio-dtmf-barge-in
content_type: documentation
product_group:
- webex-contact-center
categories:
- mcp
- webex-contact-center
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/byova-websocket-audio-dtmf-barge-in)

Understand the BYoVA WebSocket audio profile, response timing, caller barge-in, and DTMF collection behavior.

## Overview

Use this page with the [BYoVA over WebSocket guide](https://developer.webex.com/docs/bring-your-own-virtual-agent-over-websocket), which defines the full conversation contract. The media profile below reflects the current Webex Contact Center integration guidance.

## Audio format

| Property | Current integration profile |
| --- | --- |
| Encoding | G.711 mu-law, also called PCMU or u-law |
| Sample rate | 8000 Hz |
| Channels | One, mono |
| Sample size | 8 bit, one byte per sample |
| Container | None; audio content is raw and has no WAV or RIFF header |
| JSON encoding | Base64 in the audio field |

Webex sends caller audio in `audio_input.caller_audio_b64`. The partner returns audio in `prompts[].audio_content_b64`. Use the encoding and sample rate in the request, and do not add container headers to the raw media payload.

## Stream response audio

Use `CHUNK` messages for streamable response audio. Send `PARTIAL` messages for intermediate state or transcript information only when the request sets `allow_partial_responses` to `true`. That flag governs `PARTIAL`; `CHUNK` follows the separate audio-streaming behavior. Send exactly one `FINAL` to close each logical reply. A streamed response carries raw, headerless G.711 mu-law bytes in its audio fields. `FINAL` can be audio-less; do not send another response for the same reply after it.

| Fragment size | Guidance |
| --- | --- |
| Minimum | 320 bytes (40 ms at 8 kHz, mono, 8-bit) |
| Practical recommendation | 8000–16000 bytes (about 1–2 seconds) |
| Maximum | 32 KB |

Send each fragment as soon as it is generated. Webex buffers and schedules partner audio for playback, so do not pace transmission to match playback duration. If a speech engine produces frames smaller than the minimum, aggregate them until the fragment reaches the minimum, then flush.

## Speech boundaries and barge-in

The partner detects the beginning and end of caller speech and reports those boundaries to Webex:

- Send `START_OF_INPUT` when the partner detects caller speech.
- Send `END_OF_INPUT` when the partner's endpointing or end-of-turn logic considers the input complete.

Without barge-in, Webex starts the next caller-audio stream only after it receives the response `FINAL`; speech during playback is not delivered to the partner. To let the caller interrupt a prompt, set `prompts[].is_barge_in_enabled` to `true` and send `START_OF_INPUT` when new caller speech is detected. The WebSocket contract has no separate `BARGE_IN` event.

## DTMF collection

Webex delivers DTMF as one ordered `dtmf_events` collection, not one request per key. Process the digits in order. Collection ends when the configured terminator is entered, the requested maximum length is reached, or the inter-digit timeout expires.

Use `input_mode` and `input_handling_config.dtmf_config` in the partner response to configure the next input. The no-input timer applies before the first voice or DTMF input; the inter-digit timer applies after digit entry begins. Configure the digit limit, terminator, and timeout explicitly for the intended flow.

`START_OF_DTMF` is a Webex-to-partner event associated with DTMF input. In a non-barge-in DTMF turn, Webex starts the next input after `FINAL`; with barge-in enabled, the first audio-bearing response also controls when the next input stream starts.

## References

- [BYoVA over WebSocket](https://developer.webex.com/docs/bring-your-own-virtual-agent-over-websocket)
- [Published BYoVA WebSocket AsyncAPI schemas](https://github.com/webex/dataSourceSchemas/tree/main/Services/VoiceVirtualAgent_WebSocket/a38a10b7-43e4-4676-a076-a7d6dce9387d/AsyncApiSpec)
- [Java WebSocket JSON sample](https://github.com/CiscoDevNet/webex-contact-center-provider-sample-code/tree/main/bring-your-own/virtual-agent/web-socket-interface/simulators/byova-websocket-json-java)
