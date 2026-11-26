---
type: Excerpt
canonical_url: https://developer.webex.com/docs/byova-websocket-audio-dtmf-barge-in
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Speech boundaries and barge-in
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/byova-websocket-audio-dtmf-barge-in). [Full Markdown](../../../../docs/byova-websocket-audio-dtmf-barge-in.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Understand the BYoVA WebSocket audio profile, response timing, caller barge-in, and DTMF collection behavior.

## Selected section

## Speech boundaries and barge-in

The partner detects the beginning and end of caller speech and reports those boundaries to Webex:

- Send `START_OF_INPUT` when the partner detects caller speech.
- Send `END_OF_INPUT` when the partner's endpointing or end-of-turn logic considers the input complete.

Without barge-in, Webex starts the next caller-audio stream only after it receives the response `FINAL`; speech during playback is not delivered to the partner. To let the caller interrupt a prompt, set `prompts[].is_barge_in_enabled` to `true` and send `START_OF_INPUT` when new caller speech is detected. The WebSocket contract has no separate `BARGE_IN` event.
