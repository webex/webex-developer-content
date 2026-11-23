---
type: Excerpt
canonical_url: https://developer.webex.com/docs/bring-your-own-virtual-agent-over-websocket
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Requests from Webex
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/bring-your-own-virtual-agent-over-websocket). [Full Markdown](../../../../docs/bring-your-own-virtual-agent-over-websocket.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](003-before-you-begin.md) [Authentication and network requirements](011-authentication-and-network-requirements.md)

## Article introduction

Implement a partner-hosted WebSocket virtual agent that exchanges caller audio, virtual-agent responses, and conversation events with Webex Contact Center over one secure connection per conversation.

## Selected section

## Requests from Webex

Each `VOICE_VA_REQUEST` payload contains identity and configuration fields plus one input type:

```json
{
  "type": "VOICE_VA_REQUEST",
  "seq": 2,
  "ts": "2026-08-19T10:15:31Z",
  "conversation_id": "conversation-123",
  "payload": {
    "conversation_id": "conversation-123",
    "customer_org_id": "org-456",
    "virtual_agent_id": "agent-789",
    "allow_partial_responses": true,
    "vendor_specific_config": "partner-config-id",
    "voice_va_input_type": {
      "audio_input": {
        "caller_audio_b64": "<base64-encoded raw audio>",
        "encoding": "MULAW_FORMAT",
        "sample_rate_hertz": 8000,
        "language_code": "en-US"
      }
    },
    "additional_info": {
      "partner-key": "partner-value"
    }
  }
}
```

`voice_va_input_type` contains one of these objects:

| Input | Meaning |
| --- | --- |
| `audio_input` | Caller audio and its encoding, sample rate, language, and optional timestamp or single-utterance setting. |
| `dtmf_input` | Ordered DTMF digits received from the caller. |
| `event_input` | A session, interruption, no-input, or custom input event. |

Other request fields have these meanings:

| Field | Meaning |
| --- | --- |
| `customer_org_id` | Customer organization associated with the conversation. |
| `virtual_agent_id` | Selected partner virtual-agent identifier, when an agent was selected. |
| `allow_partial_responses` | Indicates whether the partner can send intermediate `PARTIAL` responses. |
| `vendor_specific_config` | Opaque partner configuration selector supplied through the integration configuration. |
| `additional_info` | Optional string-to-string context map. Treat unknown keys as optional and do not place authentication credentials or required lifecycle state in this map. |
