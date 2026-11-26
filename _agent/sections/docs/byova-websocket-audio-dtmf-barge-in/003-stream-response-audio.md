---
type: Excerpt
canonical_url: https://developer.webex.com/docs/byova-websocket-audio-dtmf-barge-in
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Stream response audio
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/byova-websocket-audio-dtmf-barge-in). [Full Markdown](../../../../docs/byova-websocket-audio-dtmf-barge-in.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Understand the BYoVA WebSocket audio profile, response timing, caller barge-in, and DTMF collection behavior.

## Selected section

## Stream response audio

Use `CHUNK` messages for streamable response audio. Send `PARTIAL` messages for intermediate state or transcript information only when the request sets `allow_partial_responses` to `true`. That flag governs `PARTIAL`; `CHUNK` follows the separate audio-streaming behavior. Send exactly one `FINAL` to close each logical reply. A streamed response carries raw, headerless G.711 mu-law bytes in its audio fields. `FINAL` can be audio-less; do not send another response for the same reply after it.

| Fragment size | Guidance |
| --- | --- |
| Minimum | 320 bytes (40 ms at 8 kHz, mono, 8-bit) |
| Practical recommendation | 8000–16000 bytes (about 1–2 seconds) |
| Maximum | 32 KB |

Send each fragment as soon as it is generated. Webex buffers and schedules partner audio for playback, so do not pace transmission to match playback duration. If a speech engine produces frames smaller than the minimum, aggregate them until the fragment reaches the minimum, then flush.
