---
type: Excerpt
canonical_url: https://developer.webex.com/docs/byova-websocket-expanded-implementation-guide
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Responsibility boundary
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/byova-websocket-expanded-implementation-guide). [Full Markdown](../../../../docs/byova-websocket-expanded-implementation-guide.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Build a partner-hosted WebSocket connector that exchanges caller input, virtual-agent responses, and lifecycle events with Webex Contact Center.

## Selected section

## Responsibility boundary

Webex Contact Center opens and manages the conversation connection, sends caller audio and input events, and handles Contact Center actions such as transfer. The partner hosts the connector, validates the bearer token, manages conversation state, detects speech boundaries, connects to its speech or agent runtime, and returns responses and output events.

`START_OF_INPUT` and `END_OF_INPUT` are partner-to-Webex events. Send them when the partner detects the caller's speech boundaries; they are not messages to the partner's agent service.
