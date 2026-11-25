---
type: Excerpt
canonical_url: https://developer.webex.com/docs/byova-websocket-troubleshooting-validation
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Connection and authentication
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/byova-websocket-troubleshooting-validation). [Full Markdown](../../../../docs/byova-websocket-troubleshooting-validation.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Use these checks to validate a partner BYoVA WebSocket connector and isolate connection, media, turn-taking, DTMF, and cleanup failures.

## Selected section

## Connection and authentication

| Symptom | Checks |
| --- | --- |
| WebSocket handshake is rejected | Confirm the endpoint is reachable over `wss://`, the certificate is valid for its hostname, and the bearer token is present and accepted. |
| The first message is rejected | Confirm `SESSION_START` is the first application input and that the request uses the expected JSON envelope. |
| Messages are associated with the wrong call | Keep one connection per `conversation_id` and return the same conversation ID in partner responses and errors. |
| Heartbeat fails | Respond promptly to `PING` with `PONG` using the same sequence number. |
