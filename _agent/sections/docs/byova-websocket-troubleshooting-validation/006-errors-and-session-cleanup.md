---
type: Excerpt
canonical_url: https://developer.webex.com/docs/byova-websocket-troubleshooting-validation
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Errors and session cleanup
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/byova-websocket-troubleshooting-validation). [Full Markdown](../../../../docs/byova-websocket-troubleshooting-validation.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Connection and authentication](002-connection-and-authentication.md)

## Article introduction

Use these checks to validate a partner BYoVA WebSocket connector and isolate connection, media, turn-taking, DTMF, and cleanup failures.

## Selected section

## Errors and session cleanup

Handle schema-defined errors such as `unauthorized`, `bad_request`, `unsupported_media`, `upstream_error`, `rate_limit`, and `timeout`. Avoid tight retry loops for rate limits and do not replay an already-started conversation unless the platform contract explicitly supports it.

On `SESSION_END`, transfer, protocol error, or transport failure, release conversation state and close the session. Keep bearer tokens, raw audio, transcripts, and other sensitive content out of error details and routine diagnostic logs.
