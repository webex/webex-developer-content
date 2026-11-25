---
type: Excerpt
canonical_url: https://developer.webex.com/docs/byova-websocket-audio-dtmf-barge-in
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- DTMF collection
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/byova-websocket-audio-dtmf-barge-in). [Full Markdown](../../../../docs/byova-websocket-audio-dtmf-barge-in.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Understand the BYoVA WebSocket audio profile, response timing, caller barge-in, and DTMF collection behavior.

## Selected section

## DTMF collection

Webex delivers DTMF as one ordered `dtmf_events` collection, not one request per key. Process the digits in order. Collection ends when the configured terminator is entered, the requested maximum length is reached, or the inter-digit timeout expires.

Use `input_mode` and `input_handling_config.dtmf_config` in the partner response to configure the next input. The no-input timer applies before the first voice or DTMF input; the inter-digit timer applies after digit entry begins. Configure the digit limit, terminator, and timeout explicitly for the intended flow.

`START_OF_DTMF` is a Webex-to-partner event associated with DTMF input. In a non-barge-in DTMF turn, Webex starts the next input after `FINAL`; with barge-in enabled, the first audio-bearing response also controls when the next input stream starts.
