---
type: Excerpt
canonical_url: https://developer.webex.com/docs/byova-websocket-protocol-reference
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Responses from the partner
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/byova-websocket-protocol-reference). [Full Markdown](../../../../docs/byova-websocket-protocol-reference.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Authentication, heartbeat, and errors](007-authentication-heartbeat-and-errors.md)

## Article introduction

Use this reference to identify BYoVA WebSocket endpoints, message envelopes, input types, response types, event directions, and error handling.

## Selected section

## Responses from the partner

`VOICE_VA_RESPONSE.payload` can contain prompts, output events, input mode, input-handling configuration, and a response type.

| Response type | Use |
| --- | --- |
| `PARTIAL` | Intermediate response content; send only when `VOICE_VA_REQUEST.payload.allow_partial_responses` is `true`. |
| `CHUNK` | Streamed response audio. |
| `FINAL` | Closes one logical reply. Send exactly one for each reply. |

A `FINAL` does not close the WebSocket or end the call. It may be audio-less. Do not send more output for that logical reply after `FINAL`.
