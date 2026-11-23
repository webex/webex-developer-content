---
type: Excerpt
canonical_url: https://developer.webex.com/docs/bring-your-own-virtual-agent-over-websocket
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Before you begin
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/bring-your-own-virtual-agent-over-websocket). [Full Markdown](../../../../docs/bring-your-own-virtual-agent-over-websocket.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Authentication and network requirements](011-authentication-and-network-requirements.md)

## Article introduction

Implement a partner-hosted WebSocket virtual agent that exchanges caller audio, virtual-agent responses, and conversation events with Webex Contact Center over one secure connection per conversation.

## Selected section

## Before you begin

Complete the common Service App, Bring Your Own Data Source (BYODS), Contact Center AI (CCAI), flow, and entry-point provisioning described in [Bring Your Own Virtual Agent](https://developer.webex.com/docs/bring-your-own-virtual-agent).

For the WebSocket variant, apply these WebSocket-specific values while completing that provisioning flow:

1. Implement the `/v1/va` and `/v1/listVirtualAgents` secure WebSocket endpoints before registering the data source.
2. In the Service App's **Bring Your Own Datasource Settings**, add the data source scopes and the partner-owned **Data Exchange Domain**.
3. Select WebSocket schema ID `a38a10b7-43e4-4676-a076-a7d6dce9387d` in **Data Exchange Schema**.
4. Register the partner WebSocket endpoint through the [Data Sources API](https://developer.webex.com/docs/api/v1/data-sources), using the same authorized Service App and schema.
5. Select that Service App and registered data source in the CCAI configuration used by the **Virtual Agent Voice** activity.

Do not create a second Service App for the WebSocket transport. The selected schema identifies the transport contract; there is no separate WebSocket protocol selector in the CCAI configuration.

If transcript publication is required, ask Webex support to enable it for the customer organization. Sending a transcript in the WebSocket response does not by itself enable transcript publication or persistence.
