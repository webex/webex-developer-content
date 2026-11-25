---
type: Excerpt
canonical_url: https://developer.webex.com/docs/bring-your-own-virtual-agent-over-websocket
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Responsibility boundary
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/bring-your-own-virtual-agent-over-websocket). [Full Markdown](../../../../docs/bring-your-own-virtual-agent-over-websocket.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](003-before-you-begin.md) [Authentication and network requirements](011-authentication-and-network-requirements.md)

## Article introduction

Implement a partner-hosted WebSocket virtual agent that exchanges caller audio, virtual-agent responses, and conversation events with Webex Contact Center over one secure connection per conversation.

## Selected section

## Responsibility boundary

The integration keeps the virtual-agent runtime and the Webex real-time session boundary separate.

| Partner owns | Webex owns |
| --- | --- |
| Hosting, operating, and supporting the partner connector | Initiating and managing the WebSocket session |
| Validating the WebSocket bearer token | Resolving the registered endpoint and credential |
| Speech recognition, end-of-turn detection, agent reasoning, and response generation | Sending caller media and Webex Contact Center input events |
| Text-to-speech or speech-to-speech media generation | Buffering and pacing partner audio to the caller |
| Mapping WebSocket events to partner runtime behavior | Applying turn finality and Webex session lifecycle rules |
| Emitting input-boundary, transfer, custom, and terminal events | Executing transfer and handoff in Webex Contact Center |
| Partner-side monitoring and operational support | Webex platform monitoring and support |

The partner maps the published WebSocket fields and events to its implementation. The partner does not implement or map Webex internal gRPC services or internal object models.
