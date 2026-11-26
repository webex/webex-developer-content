---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-control-apis
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- AgentConsulting
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-control-apis). [Full Markdown](../../../../docs/contact-control-apis.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Registering for Websocket Connection](002-registering-for-websocket-connection.md) [Common Payload Fields](003-common-payload-fields.md)

## Article introduction

---

# Contact Control APIs

When invoking the following Contact Control APIs, it is important to know that they are asynchronous and may return any of the notification payloads in this guide at any point.

## Selected section

## AgentConsulting
This is triggered when the interaction enters the consulting state.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**                | **Description**                                                                                             |
|--------------------------|-------------------------------------------------------------------------------------------------------------|
| `consultMediaResourceId` | Media resource identifier associated with the consult leg while the interaction is in the consulting state. |
| `destAgentId`            | Unique identifier of the consult destination. In the example, this is another agent identifier.             |
| `destinationType`        | Type of the consult destination. Example values: `Agent`,`DN`,`EP-DN`.                                      |

</details>

```json
{
  "type": "AgentConsulting",
  "eventType": "RoutingMessage",
  "interactionId": "d9af7d2f-cb72-4abc-974e-5484594a1c67",
  "orgId": "348adfa2-b8f0-405c-a516-da004eefde5f",
  "queueMgr": "dummy-queue-manager",
  "consultMediaResourceId": "36a854fe-86c3-42f1-9f2c-1b46ea4409da",
  "agentId": "32247eed-2b46-4b9d-a99b-9b8ba35bdc66",
  "destAgentId": "a6aa9e25-eef4-4711-a62a-a9d846916995",
  "interaction": {...},
  "trackingId": "e0c13af6-85a4-48ec-b657-b4bb1a348177",
  "destinationType": "Agent"
}
```
