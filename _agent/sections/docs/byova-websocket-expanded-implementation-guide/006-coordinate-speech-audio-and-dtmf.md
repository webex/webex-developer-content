---
type: Excerpt
canonical_url: https://developer.webex.com/docs/byova-websocket-expanded-implementation-guide
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Coordinate speech, audio, and DTMF
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/byova-websocket-expanded-implementation-guide). [Full Markdown](../../../../docs/byova-websocket-expanded-implementation-guide.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Build a partner-hosted WebSocket connector that exchanges caller input, virtual-agent responses, and lifecycle events with Webex Contact Center.

## Selected section

## Coordinate speech, audio, and DTMF

The partner owns speech-start and end-of-turn detection. Send `START_OF_INPUT` when caller speech begins and `END_OF_INPUT` when the partner's endpointing logic considers the input complete. Configure barge-in on the prompt when callers should be able to interrupt playback.

Set `input_mode` to accept DTMF on the next input. Use `input_handling_config.dtmf_config` to configure collection length, terminator, and inter-digit timeout. Webex sends the digits as one ordered collection. For media formats, response streaming, barge-in timing, and DTMF flows, see the existing BYoVA over WebSocket guide.
