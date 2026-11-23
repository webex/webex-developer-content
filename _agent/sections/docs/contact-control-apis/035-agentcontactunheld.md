---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-control-apis
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- AgentContactUnheld
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-control-apis). [Full Markdown](../../../../docs/contact-control-apis.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Registering for Websocket Connection](002-registering-for-websocket-connection.md) [Common Payload Fields](003-common-payload-fields.md)

## Article introduction

---

# Contact Control APIs

When invoking the following Contact Control APIs, it is important to know that they are asynchronous and may return any of the notification payloads in this guide at any point.

## Selected section

## AgentContactUnheld
This is triggered when a held contact is successfully resumed by an agent.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**         | **Description**                                                                                                                                                    |
|-------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `destAgentId`     | Optional destination agent identifier for consult or transfer scenarios.                                                                                           |

</details>

```json
{
  "type": "AgentContactUnheld",
  "eventType": "RoutingMessage",
  "interactionId": "8fad4d0b-60a5-4a7a-970a-762879694911",
  "orgId": "fad72201-9c4d-45fc-9c18-7d293930e581",
  "queueMgr": "queue-manager",
  "mediaResourceId": "c41d8ad5-c985-4cb4-9093-f419ea1e9ab0",
  "agentId": "8a9e031c-331f-45e8-97f7-c1dc0bf6ad79",
  "interaction": {...},
  "trackingId": "40b603bc-8ae1-4073-8c42-5a9b20662eb4",
  "destAgentId": null,
  "eventTime": 1700000003000
}
```
