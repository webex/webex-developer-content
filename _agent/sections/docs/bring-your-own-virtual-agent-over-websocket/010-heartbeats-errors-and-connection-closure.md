---
type: Excerpt
canonical_url: https://developer.webex.com/docs/bring-your-own-virtual-agent-over-websocket
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Heartbeats, errors, and connection closure
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/bring-your-own-virtual-agent-over-websocket). [Full Markdown](../../../../docs/bring-your-own-virtual-agent-over-websocket.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](003-before-you-begin.md) [Authentication and network requirements](011-authentication-and-network-requirements.md)

## Article introduction

Implement a partner-hosted WebSocket virtual agent that exchanges caller audio, virtual-agent responses, and conversation events with Webex Contact Center over one secure connection per conversation.

## Selected section

## Heartbeats, errors, and connection closure

Both sides must handle the application `PING` and `PONG` envelopes. Respond promptly to a `PING` with a `PONG` that echoes its sequence number. Heartbeat traffic maintains transport liveness; heartbeat sequence values are not turn identifiers.

The partner can send an `ERROR` envelope with a schema-defined code, numeric status, and bounded detail:

| Code | Use when |
| --- | --- |
| `unauthorized` | The bearer token or partner authorization was rejected. |
| `bad_request` | The request is invalid for the current protocol or session state. |
| `unsupported_media` | The encoding, sample rate, or media content is unsupported. |
| `upstream_error` | The partner's agent, speech, or other upstream service failed. |
| `rate_limit` | Partner capacity or quota is exhausted. |
| `timeout` | A partner operation exceeded its time limit. |

Do not include credentials, raw audio, transcripts, or other sensitive content in `detail`.

A failed WebSocket handshake, heartbeat timeout, malformed known envelope, mismatched `conversation_id`, unexpected connection close, or mid-session network failure ends the current virtual-agent session. Even when an error is classified as potentially retryable, Webex does not reconnect and replay the existing WebSocket session automatically.
