---
type: Excerpt
canonical_url: https://developer.webex.com/docs/byova-websocket-audio-dtmf-barge-in
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Audio format
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/byova-websocket-audio-dtmf-barge-in). [Full Markdown](../../../../docs/byova-websocket-audio-dtmf-barge-in.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Understand the BYoVA WebSocket audio profile, response timing, caller barge-in, and DTMF collection behavior.

## Selected section

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
