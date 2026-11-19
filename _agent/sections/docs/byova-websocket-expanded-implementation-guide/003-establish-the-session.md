---
type: Excerpt
canonical_url: https://developer.webex.com/docs/byova-websocket-expanded-implementation-guide
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Establish the session
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/byova-websocket-expanded-implementation-guide). [Full Markdown](../../../../docs/byova-websocket-expanded-implementation-guide.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Build a partner-hosted WebSocket connector that exchanges caller input, virtual-agent responses, and lifecycle events with Webex Contact Center.

## Selected section

## Establish the session

1. Expose the partner connector at a publicly reachable `wss://` endpoint with a valid TLS certificate.
2. Accept the WebSocket upgrade and validate the bearer token before processing application messages.
3. Use one connection for one `conversation_id` and keep it open across turns. Do not multiplex conversations on a connection.
4. Treat `SESSION_START` in the first `VOICE_VA_REQUEST` as the start of application state. A welcome response may follow before caller audio arrives.

The `/v1/va` endpoint carries conversation traffic. Implement `/v1/listVirtualAgents` separately for virtual-agent discovery; its request and response do not use the conversation envelope.
