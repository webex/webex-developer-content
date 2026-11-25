---
type: Excerpt
canonical_url: https://developer.webex.com/docs/byova-websocket-troubleshooting-validation
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- End-to-end checklist
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/byova-websocket-troubleshooting-validation). [Full Markdown](../../../../docs/byova-websocket-troubleshooting-validation.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Connection and authentication](002-connection-and-authentication.md)

## Article introduction

Use these checks to validate a partner BYoVA WebSocket connector and isolate connection, media, turn-taking, DTMF, and cleanup failures.

## Selected section

## End-to-end checklist

- [ ] The authenticated secure WebSocket handshake succeeds.
- [ ] `SESSION_START` initializes one conversation on one connection.
- [ ] Caller audio is decoded with the encoding and sample rate supplied by Webex.
- [ ] Speech boundaries are reported to Webex.
- [ ] Audio fragments follow the current media profile and are sent without artificial pacing.
- [ ] For the next caller input, `input_mode` is correct and `input_handling_config` supplies any needed DTMF collection settings or speech timers.
- [ ] Exactly one `FINAL` closes each logical reply.
- [ ] Barge-in and non-barge-in timing match the configured prompt behavior.
- [ ] DTMF digits are collected and processed in order.
- [ ] `PING` receives a matching `PONG`.
- [ ] Exit events release state and close the session.
