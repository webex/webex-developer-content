---
type: Excerpt
canonical_url: https://developer.webex.com/docs/byova-websocket-expanded-implementation-guide
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Handle errors and close the session
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/byova-websocket-expanded-implementation-guide). [Full Markdown](../../../../docs/byova-websocket-expanded-implementation-guide.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Build a partner-hosted WebSocket connector that exchanges caller input, virtual-agent responses, and lifecycle events with Webex Contact Center.

## Selected section

## Handle errors and close the session

Return only schema-defined error codes and bounded details. Do not put bearer tokens, raw audio, transcripts, or other sensitive content in error details. Avoid tight retry loops for rate limits. Webex does not reconnect and replay an established conversation after a connection failure.

Release conversation state and close the session on `SESSION_END`, transfer, protocol error, or transport failure. Respond promptly to `PING` with `PONG` using the same sequence number.
