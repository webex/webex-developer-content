---
type: Excerpt
canonical_url: https://developer.webex.com/docs/byova-websocket-protocol-reference
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Conversation message envelope
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/byova-websocket-protocol-reference). [Full Markdown](../../../../docs/byova-websocket-protocol-reference.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Authentication, heartbeat, and errors](007-authentication-heartbeat-and-errors.md)

## Article introduction

Use this reference to identify BYoVA WebSocket endpoints, message envelopes, input types, response types, event directions, and error handling.

## Selected section

## Conversation message envelope

A conversation message is a JSON text frame. The common envelope contains:

| Field | Meaning |
| --- | --- |
| `type` | Message kind, such as `VOICE_VA_REQUEST`, `VOICE_VA_RESPONSE`, `PING`, `PONG`, or `ERROR`. |
| `seq` | Sender-owned sequence number. It is not a turn number or request-response correlation ID. |
| `ts` | RFC 3339 message timestamp. |
| `conversation_id` | Stable conversation identity for the WebSocket session. |
| `payload` | Request or response body for voice messages. Heartbeat and error messages use their schema-defined top-level fields. |

Example `SESSION_START` request with the required payload fields:

```json
{
  "type": "VOICE_VA_REQUEST",
  "seq": 1,
  "ts": "2026-08-19T10:15:31Z",
  "conversation_id": "conversation-123",
  "payload": {
    "conversation_id": "conversation-123",
    "customer_org_id": "org-123",
    "voice_va_input_type": {
      "event_input": {
        "event_type": "SESSION_START"
      }
    }
  }
}
```

Each sender maintains an independent increasing sequence counter for application messages. A `PONG` echoes the `seq` from the corresponding `PING`.
