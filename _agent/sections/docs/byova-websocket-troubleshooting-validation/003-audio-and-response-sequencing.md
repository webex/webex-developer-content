---
type: Excerpt
canonical_url: https://developer.webex.com/docs/byova-websocket-troubleshooting-validation
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Audio and response sequencing
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/byova-websocket-troubleshooting-validation). [Full Markdown](../../../../docs/byova-websocket-troubleshooting-validation.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Connection and authentication](002-connection-and-authentication.md)

## Article introduction

Use these checks to validate a partner BYoVA WebSocket connector and isolate connection, media, turn-taking, DTMF, and cleanup failures.

## Selected section

## Audio and response sequencing

| Symptom | Checks |
| --- | --- |
| Audio is rejected or sounds wrong | Confirm raw G.711 mu-law/PCMU, 8 kHz, mono audio. Keep the payload Base64-encoded inside JSON and do not add a WAV or RIFF header. |
| Response starts late or sounds choppy | Send each audio fragment as soon as it is generated; do not pace transmission to playback duration. Check the 320-byte minimum and 32 KB maximum. |
| Streamed audio is malformed | Confirm chunk audio contains raw, headerless media bytes and the response follows the published AsyncAPI schema. |
| A reply never completes or repeats | Send `PARTIAL` only when the request sets `allow_partial_responses` to true; use `CHUNK` for streamed audio independently. Then send exactly one `FINAL` and no more output for that reply. |
