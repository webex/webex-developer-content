---
type: Excerpt
canonical_url: https://developer.webex.com/docs/bring-your-own-virtual-agent-over-websocket
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- List virtual agents
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/bring-your-own-virtual-agent-over-websocket). [Full Markdown](../../../../docs/bring-your-own-virtual-agent-over-websocket.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](003-before-you-begin.md) [Authentication and network requirements](011-authentication-and-network-requirements.md)

## Article introduction

Implement a partner-hosted WebSocket virtual agent that exchanges caller audio, virtual-agent responses, and conversation events with Webex Contact Center over one secure connection per conversation.

## Selected section

## List virtual agents

Implement `/v1/listVirtualAgents` separately from the conversation endpoint. It uses the [List Virtual Agents AsyncAPI contract](https://github.com/webex/dataSourceSchemas/blob/main/Services/VoiceVirtualAgent_WebSocket/a38a10b7-43e4-4676-a076-a7d6dce9387d/AsyncApiSpec/VoiceVirtualAgent_WsListVASchema.json).

The request contains:

- Required `customer_org_id`.
- Optional `is_default_virtual_agent_enabled`.

The response contains a `virtual_agents` array. Each entry contains a required `id` and `name` and an optional `description`. The `id` is returned as `virtual_agent_id` on a conversation request when that virtual agent is selected.

Do not wrap these messages in the `/v1/va` `VOICE_VA_REQUEST` or `VOICE_VA_RESPONSE` envelope, and do not apply the one-connection-per-`conversation_id` rule to this endpoint.
