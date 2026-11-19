---
type: Excerpt
canonical_url: https://developer.webex.com/docs/bring-your-own-virtual-agent-over-websocket
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Frequently asked questions
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/bring-your-own-virtual-agent-over-websocket). [Full Markdown](../../../../docs/bring-your-own-virtual-agent-over-websocket.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](003-before-you-begin.md) [Authentication and network requirements](011-authentication-and-network-requirements.md)

## Article introduction

Implement a partner-hosted WebSocket virtual agent that exchanges caller audio, virtual-agent responses, and conversation events with Webex Contact Center over one secure connection per conversation.

## Selected section

## Frequently asked questions

### Who opens the WebSocket?

Webex opens the connection to the partner-hosted endpoint.

### Is there one WebSocket per turn?

No. There is one WebSocket for the conversation, and it carries multiple turns until the conversation ends.

### Can one WebSocket carry multiple conversations?

No. Do not multiplex conversation IDs on one connection.

### What is the first message?

A `VOICE_VA_REQUEST` containing `SESSION_START`. The partner can respond with welcome text or audio before caller audio arrives.

### What ends a virtual-agent turn?

The first valid `FINAL` for that logical partner reply. `FINAL` does not close the WebSocket or end the call.

### Who detects the end of caller speech?

The partner. Map the partner's voice activity, speech recognition, or speech-to-speech turn detector to `START_OF_INPUT` and `END_OF_INPUT` output events.

### Are barge-in, DTMF, and agent handoff supported?

Yes. Use `is_barge_in_enabled` and input-boundary events for voice interruption, `dtmf_input` for digits, and `TRANSFER_TO_AGENT` for handoff.

### Should the partner pace audio in real time?

No. Send chunks as soon as they are generated. Webex buffers and paces playback to the caller.

### Can the partner send WAV audio?

No. Send raw codec bytes without WAV, RIFF, or another container header.

### Does every codec enum in the schema work end to end?

No. Use the qualified media profile in this guide unless Webex approves a different profile for the integration.

### Can a speech-to-speech model connect without an adapter?

Only if it natively satisfies every media, event, turn, finality, and lifecycle requirement. Most implementations need a partner adapter.

### Is mTLS required?

No. WebSocket currently uses server-authenticated TLS and bearer-token validation. Optional BYOVA mTLS is gRPC-only.

### Will Webex reconnect after a network drop?

No. There is no automatic reconnect, resume, or replay for the existing conversation WebSocket.

### Is `conversation_id` a turn identifier?

No. It identifies the conversation and WebSocket session. Turn progression is carried by inputs, responses, events, and `FINAL`.

### Can the partner send binary WebSocket frames?

No. Send JSON text frames and carry audio as Base64 in the schema-defined fields.

### Are custom events supported?

Yes. Both directions support `CUSTOM_EVENT`. Agree on the event name, parameter or metadata shape, size, and ownership before relying on it.

### Are transcripts always published or stored?

No. Transcript publication is customer-organization configuration dependent. Sending `session_transcript` does not by itself guarantee persistence or display.

### Can the partner return a post-call summary?

The schema includes `session_summary`, but it is not a supported substitute for the accumulated Webex handoff transcript. Do not depend on it being persisted or displayed.
