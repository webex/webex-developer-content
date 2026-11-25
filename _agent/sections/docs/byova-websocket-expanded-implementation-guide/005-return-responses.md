---
type: Excerpt
canonical_url: https://developer.webex.com/docs/byova-websocket-expanded-implementation-guide
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Return responses
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/byova-websocket-expanded-implementation-guide). [Full Markdown](../../../../docs/byova-websocket-expanded-implementation-guide.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Build a partner-hosted WebSocket connector that exchanges caller input, virtual-agent responses, and lifecycle events with Webex Contact Center.

## Selected section

## Return responses

Send a `VOICE_VA_RESPONSE` with the next partner sequence number, the same `conversation_id`, and the output needed for the current turn. When the request sets `allow_partial_responses` to true, a logical reply can contain zero or more `PARTIAL` messages. Use `CHUNK` for streamed response audio independently, then send exactly one `FINAL`. Do not send another response for that reply after `FINAL`; it closes the reply, not the WebSocket or the call.

Use `output_events` for partner-to-Webex events, including speech boundaries and agreed Contact Center actions. Set `input_mode` to choose the next accepted caller input; use `input_handling_config` for its collection settings.
