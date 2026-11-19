---
type: Excerpt
canonical_url: https://developer.webex.com/docs/bring-your-own-virtual-agent-over-websocket
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Validate the implementation
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/bring-your-own-virtual-agent-over-websocket). [Full Markdown](../../../../docs/bring-your-own-virtual-agent-over-websocket.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](003-before-you-begin.md) [Authentication and network requirements](011-authentication-and-network-requirements.md)

## Article introduction

Implement a partner-hosted WebSocket virtual agent that exchanges caller audio, virtual-agent responses, and conversation events with Webex Contact Center over one secure connection per conversation.

## Selected section

## Validate the implementation

Before production onboarding, validate these scenarios end to end:

1. Webex establishes `wss` with a valid bearer token and the partner rejects invalid authentication.
2. `SESSION_START` is the first application request and the partner can return a welcome response.
3. Caller audio is decoded as raw G.711 mu-law at 8 kHz without a WAV or RIFF header.
4. The partner streams response chunks without artificial playback pacing and sends exactly one `FINAL` per reply.
5. Multiple caller and virtual-agent turns use the same WebSocket connection.
6. Voice barge-in stops interruptible playback and produces the expected input-boundary sequence.
7. DTMF digits retain their order and the configured termination behavior works.
8. `NO_INPUT`, `NO_MATCH`, and custom events are mapped correctly.
9. `TRANSFER_TO_AGENT` ends the virtual-agent leg and follows the configured handoff path.
10. `PING` receives `PONG`, and a missing heartbeat response is observable.
11. A partner `ERROR`, malformed frame, or connection drop ends the current session without replay.
12. `SESSION_END` closes the application session cleanly.
13. When transcript publication is enabled, final transcript content reaches the intended downstream experience without exposing sensitive input.
