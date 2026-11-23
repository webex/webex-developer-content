---
type: Excerpt
canonical_url: https://developer.webex.com/docs/byova-websocket-expanded-implementation-guide
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Validate the connector
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/byova-websocket-expanded-implementation-guide). [Full Markdown](../../../../docs/byova-websocket-expanded-implementation-guide.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Build a partner-hosted WebSocket connector that exchanges caller input, virtual-agent responses, and lifecycle events with Webex Contact Center.

## Selected section

## Validate the connector

- Confirm the authenticated `wss://` handshake and first `SESSION_START` request.
- Confirm one connection carries multiple turns for one conversation.
- Confirm audio, DTMF, and event inputs dispatch to the correct partner behavior.
- Confirm speech-boundary events, output sequencing, and one `FINAL` per reply.
- Confirm `PING` receives a matching `PONG` and exit events release state.
