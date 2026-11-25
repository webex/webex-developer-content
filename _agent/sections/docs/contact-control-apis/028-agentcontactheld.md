---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-control-apis
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- AgentContactHeld
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-control-apis). [Full Markdown](../../../../docs/contact-control-apis.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Registering for Websocket Connection](002-registering-for-websocket-connection.md) [Common Payload Fields](003-common-payload-fields.md)

## Article introduction

---

# Contact Control APIs

When invoking the following Contact Control APIs, it is important to know that they are asynchronous and may return any of the notification payloads in this guide at any point.

## Selected section

## AgentContactHeld
This is triggered when an active contact is successfully placed on hold by an agent.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Description**                                                                                                                                                                 |
|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `destAgentId` - Optional destination agent identifier for consult or transfer scenarios, when applicable.                                                                       |

</details>

```json
{
  "type": "AgentContactHeld",
  "eventType": "RoutingMessage",
  "interactionId": "7d2491bc-0dae-4c73-8969-f642d590b703",
  "orgId": "2e78188d-2c0d-4c2a-9408-9bd7436095c7",
  "queueMgr": "queue-manager",
  "mediaResourceId": "25deaac7-dd61-42aa-a165-c2124f7a326a",
  "agentId": "3ab74c76-4651-4c8c-9a47-0ca60a716680",
  "interaction": {...},
  "trackingId": "2895e095-a03e-4dd7-8332-7c1cad64a64f",
  "destAgentId": "a74b5306-c898-46b6-9546-cee687286aea",
  "eventTime": 1700000002000
}
```
