---
type: Excerpt
canonical_url: https://developer.webex.com/docs/byova-websocket-expanded-implementation-guide
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Process requests
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/byova-websocket-expanded-implementation-guide). [Full Markdown](../../../../docs/byova-websocket-expanded-implementation-guide.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Build a partner-hosted WebSocket connector that exchanges caller input, virtual-agent responses, and lifecycle events with Webex Contact Center.

## Selected section

## Process requests

Validate the message envelope and dispatch the single input type carried by `voice_va_input_type`.

| Input | Connector behavior |
| --- | --- |
| `audio_input` | Decode the Base64 caller audio and use the media properties supplied by Webex. |
| `dtmf_input` | Process the ordered DTMF collection as one input. |
| `event_input` | Handle lifecycle or control events such as `SESSION_START`, `NO_INPUT`, and `CUSTOM_EVENT`. |

Keep conversation identity stable for the connection. Maintain the partner's own increasing sequence number for its application responses; it is not a turn number or a copy of the request sequence.
