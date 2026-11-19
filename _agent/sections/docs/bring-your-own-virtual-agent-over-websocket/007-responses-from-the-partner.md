---
type: Excerpt
canonical_url: https://developer.webex.com/docs/bring-your-own-virtual-agent-over-websocket
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Responses from the partner
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/bring-your-own-virtual-agent-over-websocket). [Full Markdown](../../../../docs/bring-your-own-virtual-agent-over-websocket.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](003-before-you-begin.md) [Authentication and network requirements](011-authentication-and-network-requirements.md)

## Article introduction

Implement a partner-hosted WebSocket virtual agent that exchanges caller audio, virtual-agent responses, and conversation events with Webex Contact Center over one secure connection per conversation.

## Selected section

## Responses from the partner

The partner sends virtual-agent output in `VOICE_VA_RESPONSE` messages:

```json
{
  "type": "VOICE_VA_RESPONSE",
  "seq": 8,
  "ts": "2026-08-19T10:15:32Z",
  "conversation_id": "conversation-123",
  "payload": {
    "prompts": [
      {
        "audio_content_b64": "<base64-encoded raw audio>",
        "is_barge_in_enabled": true
      }
    ],
    "output_events": [],
    "input_mode": "INPUT_VOICE_DTMF",
    "input_sensitive": false,
    "response_type": "CHUNK"
  }
}
```

| Field | Meaning |
| --- | --- |
| `prompts` | Text and inline audio to play to the caller. For streamed audio, use `audio_content_b64`. |
| `output_events` | Input-boundary, transfer, custom, no-input, no-match, or terminal events produced by the partner. |
| `input_mode` | Input accepted for the next interaction: voice, DTMF, or both. |
| `input_handling_config` | DTMF collection settings and speech timers for subsequent caller input. |
| `input_sensitive` | Marks sensitive virtual-agent output so Webex can apply secure-result handling. |
| `session_transcript` | Optional caller transcript content. Transcript publication remains customer-organization configuration dependent. |
| `session_summary` | Present in the schema, but not a supported substitute for the Webex handoff transcript. Do not depend on a partner-provided summary being persisted or displayed. |
| `disable_prompt_cancellation` | Prevents a partial automated-agent reply from being canceled by a later partner reply. It is separate from caller barge-in behavior. |
| `response_type` | `PARTIAL`, `CHUNK`, or `FINAL`. |

### Response finality

A logical virtual-agent reply can contain:

- Zero or more `PARTIAL` responses for intermediate state or transcript information.
- Zero or more `CHUNK` responses carrying streamable reply audio.
- Exactly one `FINAL` response.

The `FINAL` response can have no audio, for example when completing an event-only response. Do not send multiple `FINAL` responses for one reply. Input-boundary events such as `START_OF_INPUT`, `END_OF_INPUT`, `NO_INPUT`, and `NO_MATCH` describe recognition state and do not by themselves end the entire conversation.
