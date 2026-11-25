---
type: Excerpt
canonical_url: https://developer.webex.com/docs/bring-your-own-virtual-agent-over-websocket
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Message envelope
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/bring-your-own-virtual-agent-over-websocket). [Full Markdown](../../../../docs/bring-your-own-virtual-agent-over-websocket.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](003-before-you-begin.md) [Authentication and network requirements](011-authentication-and-network-requirements.md)

## Article introduction

Implement a partner-hosted WebSocket virtual agent that exchanges caller audio, virtual-agent responses, and conversation events with Webex Contact Center over one secure connection per conversation.

## Selected section

## Message envelope

Messages on `/v1/va` are JSON text frames. Audio is Base64-encoded inside the JSON payload; binary WebSocket frames are not part of this contract.

The common envelope is:

```json
{
  "type": "VOICE_VA_REQUEST",
  "seq": 1,
  "ts": "2026-08-19T10:15:30Z",
  "conversation_id": "conversation-123",
  "payload": {}
}
```

| Field | Required behavior |
| --- | --- |
| `type` | Identifies the message as `VOICE_VA_REQUEST`, `VOICE_VA_RESPONSE`, `ERROR`, `PING`, or `PONG`. |
| `seq` | Positive, monotonically increasing counter owned independently by each sender for the connection. It is not a turn number or request-response correlation ID. Sequence gaps are permitted. |
| `ts` | Message creation time in RFC 3339 date-time format. |
| `conversation_id` | Stable identity of the conversation and WebSocket session. Return the same nonempty value on partner response and error envelopes. |
| `metadata` | Optional extension data. Do not use it for required authentication, media, turn, or lifecycle semantics. |
| `payload` | Request or response body for the message type. `PING`, `PONG`, and `ERROR` use their schema-defined envelope fields. |

The partner must use its own increasing sequence counter across all application responses on the connection. Do not copy the request sequence number into a `VOICE_VA_RESPONSE`. For heartbeat traffic, a `PONG` echoes the corresponding `PING` sequence number.
