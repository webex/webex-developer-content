---
type: Excerpt
canonical_url: https://developer.webex.com/docs/byova-websocket-protocol-reference
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Event directions
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/byova-websocket-protocol-reference). [Full Markdown](../../../../docs/byova-websocket-protocol-reference.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Authentication, heartbeat, and errors](007-authentication-heartbeat-and-errors.md)

## Article introduction

Use this reference to identify BYoVA WebSocket endpoints, message envelopes, input types, response types, event directions, and error handling.

## Selected section

## Event directions

| Direction | Event examples |
| --- | --- |
| Webex to partner | `SESSION_START`, `SESSION_END`, `NO_INPUT`, `START_OF_DTMF`, `CUSTOM_EVENT` |
| Partner to Webex | `START_OF_INPUT`, `END_OF_INPUT`, `NO_MATCH`, `NO_INPUT`, `CUSTOM_EVENT`, `TRANSFER_TO_AGENT`, `SESSION_END` |

`START_OF_INPUT` and `END_OF_INPUT` are partner-to-Webex input-boundary events. The partner sends them based on its speech detection and end-of-turn logic. `SESSION_END` can be sent in either direction to end the application session.
