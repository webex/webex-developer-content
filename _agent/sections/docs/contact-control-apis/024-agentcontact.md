---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-control-apis
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- AgentContact
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-control-apis). [Full Markdown](../../../../docs/contact-control-apis.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Registering for Websocket Connection](002-registering-for-websocket-connection.md) [Common Payload Fields](003-common-payload-fields.md)

## Article introduction

---

# Contact Control APIs

When invoking the following Contact Control APIs, it is important to know that they are asynchronous and may return any of the notification payloads in this guide at any point.

## Selected section

## AgentContact
This is triggered during agent reload/relogin recovery when contact details are fetched for active interactions already assigned to the agent.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**                | **Description**                                                                                                                 |
|--------------------------|---------------------------------------------------------------------------------------------------------------------------------|
| `isConsulted`            | Indicates whether the agent is joined as a consulted participant for this interaction.                                          |
| `consultMediaResourceId` | Media resource identifier for the consult leg, when available.                                                                  |
| `reservedAgentChannelId` | Reserved channel identifier for campaign reservation scenarios, when available.                                                 |

</details>

```json
{
  "type": "AgentContact",
  "eventType": "RoutingMessage",
  "interactionId": "5a3c1e9d-7b42-4f8a-9d6c-2e1f3a4b5c6d",
  "orgId": "1f2e3d4c-5b6a-4a8d-9c1e-7b2a3c4d5e6f",
  "queueMgr": "queue-manager",
  "agentId": "9c7d6e5f-3a2b-4f8d-8e1c-0b9a7d6e5f4c",
  "isConsulted": false,
  "mediaResourceId": "6e5d4c3b-2a1f-4e8d-9c0b-3a2b1c4d5e6f",
  "consultMediaResourceId": null,
  "interaction": {...},
  "trackingId": "2b3c4d5e-6f7a-4a8d-b9c1-3e2f1a4b5c6d",
  "reservedAgentChannelId": null,
  "eventTime": 1700000013000
}
```
