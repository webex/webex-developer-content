---
type: Excerpt
canonical_url: https://developer.webex.com/docs/bring-your-own-virtual-agent-over-websocket
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Audio format and chunking
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/bring-your-own-virtual-agent-over-websocket). [Full Markdown](../../../../docs/bring-your-own-virtual-agent-over-websocket.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](003-before-you-begin.md) [Authentication and network requirements](011-authentication-and-network-requirements.md)

## Article introduction

Implement a partner-hosted WebSocket virtual agent that exchanges caller audio, virtual-agent responses, and conversation events with Webex Contact Center over one secure connection per conversation.

## Selected section

## Audio format and chunking

Use the following media profile for the current Webex Contact Center integration:

| Property | Value |
| --- | --- |
| Encoding | Raw G.711 mu-law, also called PCMU or u-law |
| Sample rate | 8000 Hz |
| Channels | One, mono |
| Sample size | 8 bit, one byte per sample |
| Container | None; do not include WAV, RIFF, or other container headers |
| WebSocket encoding | Base64 inside the JSON field |
| Recommended raw chunk size | 8000-16000 bytes, representing 1-2 seconds of audio |
| Minimum raw chunk size | 320 bytes, representing 40 milliseconds of audio |
| Maximum raw chunk size | 32 KB |
| Delivery | Send each chunk as soon as it is generated; do not pace transmission to playback speed |

Webex sends caller audio in `audio_input.caller_audio_b64`. The partner returns audio in `prompts[].audio_content_b64`.

Start returning audio as soon as the first response chunk is available. Do not wait for the complete response, add leading silence, or delay each chunk according to its playback duration. Webex buffers and paces partner audio for caller playback.

The AsyncAPI schema exposes additional encoding enum values. Their presence in the schema does not establish end-to-end qualification for every codec or sample rate. Use the media profile documented in this section unless Webex has approved a different profile for the integration.
