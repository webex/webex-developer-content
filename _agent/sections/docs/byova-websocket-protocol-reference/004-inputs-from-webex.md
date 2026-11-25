---
type: Excerpt
canonical_url: https://developer.webex.com/docs/byova-websocket-protocol-reference
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Inputs from Webex
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/byova-websocket-protocol-reference). [Full Markdown](../../../../docs/byova-websocket-protocol-reference.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Authentication, heartbeat, and errors](007-authentication-heartbeat-and-errors.md)

## Article introduction

Use this reference to identify BYoVA WebSocket endpoints, message envelopes, input types, response types, event directions, and error handling.

## Selected section

## Inputs from Webex

`VOICE_VA_REQUEST.payload.voice_va_input_type` contains one input object:

| Input | Meaning |
| --- | --- |
| `audio_input` | Caller audio and media properties. Audio is Base64-encoded in JSON. |
| `dtmf_input` | An ordered collection of DTMF events. |
| `event_input` | A lifecycle or control event, such as `SESSION_START`, `NO_INPUT`, or `CUSTOM_EVENT`. |

`SESSION_START` is the first application input on a conversation connection. Other event examples include `SESSION_END`, `START_OF_DTMF`, and `CUSTOM_EVENT`.
