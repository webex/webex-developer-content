---
type: Excerpt
canonical_url: https://developer.webex.com/docs/byova-websocket-protocol-reference
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Authentication, heartbeat, and errors
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/byova-websocket-protocol-reference). [Full Markdown](../../../../docs/byova-websocket-protocol-reference.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Use this reference to identify BYoVA WebSocket endpoints, message envelopes, input types, response types, event directions, and error handling.

## Selected section

## Authentication, heartbeat, and errors

Validate the bearer token during the WebSocket upgrade before processing application messages. Respond promptly to `PING` with `PONG` and the matching sequence number.

Partner error envelopes use schema-defined codes, including `unauthorized`, `bad_request`, `unsupported_media`, `upstream_error`, `rate_limit`, and `timeout`. Keep error details bounded and do not include credentials, raw audio, transcripts, or other sensitive content.
