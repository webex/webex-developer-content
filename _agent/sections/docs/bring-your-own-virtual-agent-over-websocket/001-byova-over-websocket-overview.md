---
type: Excerpt
canonical_url: https://developer.webex.com/docs/bring-your-own-virtual-agent-over-websocket
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- BYOVA over WebSocket overview
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/bring-your-own-virtual-agent-over-websocket). [Full Markdown](../../../../docs/bring-your-own-virtual-agent-over-websocket.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](003-before-you-begin.md) [Authentication and network requirements](011-authentication-and-network-requirements.md)

## Article introduction

Implement a partner-hosted WebSocket virtual agent that exchanges caller audio, virtual-agent responses, and conversation events with Webex Contact Center over one secure connection per conversation.

## Selected section

## BYOVA over WebSocket overview

Bring Your Own Virtual Agent (BYOVA) over WebSocket provides a bidirectional, JSON-based contract between Webex Contact Center and a partner-hosted virtual-agent connector. Webex initiates and manages the WebSocket session. The partner hosts and supports the connector and owns its speech, agent, and response-generation stack.

The partner implementation can use a modular speech-to-text, agent or large language model, and text-to-speech pipeline, or a voice-native speech-to-speech model. The implementation must adapt that stack to the WebSocket media, event, turn, and lifecycle contract. A speech-to-speech model is not automatically compatible only because it accepts and produces audio.

The WebSocket contract has two endpoints:

| Endpoint | Purpose | Connection scope | Message types |
| --- | --- | --- | --- |
| `/v1/va` | Run a voice virtual-agent conversation | One connection for each `conversation_id`, reused for all turns in that conversation | `VOICE_VA_REQUEST`, `VOICE_VA_RESPONSE`, `ERROR`, `PING`, and `PONG` |
| `/v1/listVirtualAgents` | Return the virtual agents available to an organization | A separate request-response connection; the conversation connection rules do not apply | `ListVARequest` and `ListVAResponse` |

Use the published [BYOVA WebSocket AsyncAPI specifications](https://github.com/webex/dataSourceSchemas/tree/main/Services/VoiceVirtualAgent_WebSocket/a38a10b7-43e4-4676-a076-a7d6dce9387d/AsyncApiSpec) as the source of truth for JSON field names, types, required fields, and enum values. This guide describes the lifecycle and behavior that the schema alone does not explain.
