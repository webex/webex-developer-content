---
type: Excerpt
canonical_url: https://developer.webex.com/docs/byova-websocket-troubleshooting-validation
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Voice and barge-in
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/byova-websocket-troubleshooting-validation). [Full Markdown](../../../../docs/byova-websocket-troubleshooting-validation.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Connection and authentication](002-connection-and-authentication.md)

## Article introduction

Use these checks to validate a partner BYoVA WebSocket connector and isolate connection, media, turn-taking, DTMF, and cleanup failures.

## Selected section

## Voice and barge-in

- Send `START_OF_INPUT` when the partner detects caller speech and `END_OF_INPUT` when its endpointing logic considers the speech complete.
- Without barge-in, expect the next caller-audio stream after `FINAL`; speech spoken while the prompt plays is not delivered to the partner.
- For caller interruption, enable `prompts[].is_barge_in_enabled` and report detected speech with `START_OF_INPUT`.
- Do not wait for a literal `BARGE_IN` event; the WebSocket contract uses the prompt setting and input-boundary events.
