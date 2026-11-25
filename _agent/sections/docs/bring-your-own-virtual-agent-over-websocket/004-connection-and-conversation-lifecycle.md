---
type: Excerpt
canonical_url: https://developer.webex.com/docs/bring-your-own-virtual-agent-over-websocket
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Connection and conversation lifecycle
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/bring-your-own-virtual-agent-over-websocket). [Full Markdown](../../../../docs/bring-your-own-virtual-agent-over-websocket.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](003-before-you-begin.md) [Authentication and network requirements](011-authentication-and-network-requirements.md)

## Article introduction

Implement a partner-hosted WebSocket virtual agent that exchanges caller audio, virtual-agent responses, and conversation events with Webex Contact Center over one secure connection per conversation.

## Selected section

## Connection and conversation lifecycle

Webex opens one `wss` connection to `/v1/va` for one `conversation_id`. The connection can carry a welcome response followed by multiple caller and virtual-agent turns. Do not open a new connection for each turn, and do not multiplex multiple conversations on one connection.

A typical conversation follows this sequence:

1. Webex opens the secure WebSocket connection and sends the bearer token in the HTTP `Authorization` header.
2. Webex sends a `VOICE_VA_REQUEST` containing `SESSION_START` as the first application message. This message normally uses envelope sequence number `1` and contains no synthetic audio.
3. The partner can send a welcome response as one or more `PARTIAL` or `CHUNK` responses followed by one `FINAL` response.
4. Webex sends caller audio, DTMF, or input events in subsequent `VOICE_VA_REQUEST` messages.
5. The partner detects caller input boundaries and sends virtual-agent audio, transcript content when applicable, and output events in `VOICE_VA_RESPONSE` messages.
6. The partner sends exactly one `FINAL` for each logical reply. `FINAL` ends that reply, not the conversation or WebSocket connection.
7. The same connection continues with the next caller turn.
8. A transfer, application `SESSION_END`, call end, protocol failure, or transport failure ends the session. On an orderly Webex-initiated end, Webex sends one application `SESSION_END` before closing the WebSocket.

After the WebSocket connection is established, the current session is not automatically reconnected, resumed, or replayed following a connection failure. The partner must not depend on Webex replaying earlier audio, events, or turns.
