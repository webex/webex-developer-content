---
type: Excerpt
canonical_url: https://developer.webex.com/docs/byova-websocket-protocol-reference
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Endpoints
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/byova-websocket-protocol-reference). [Full Markdown](../../../../docs/byova-websocket-protocol-reference.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Authentication, heartbeat, and errors](007-authentication-heartbeat-and-errors.md)

## Article introduction

Use this reference to identify BYoVA WebSocket endpoints, message envelopes, input types, response types, event directions, and error handling.

## Selected section

## Endpoints

| Endpoint | Purpose |
| --- | --- |
| `/v1/va` | Bidirectional conversation traffic, including requests, responses, heartbeat messages, and errors. |
| `/v1/listVirtualAgents` | Separate discovery operation that returns virtual agents available to an organization. |

Use one secure WebSocket connection for one `conversation_id`. Keep it open across turns and do not multiplex conversations on the same connection. Virtual-agent discovery is a separate request-response operation and does not use the conversation envelope.
