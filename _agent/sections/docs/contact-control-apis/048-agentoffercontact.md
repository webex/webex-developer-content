---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-control-apis
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- AgentOfferContact
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-control-apis). [Full Markdown](../../../../docs/contact-control-apis.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Registering for Websocket Connection](002-registering-for-websocket-connection.md) [Common Payload Fields](003-common-payload-fields.md)

## Article introduction

---

# Contact Control APIs

When invoking the following Contact Control APIs, it is important to know that they are asynchronous and may return any of the notification payloads in this guide at any point.

## Selected section

## AgentOfferContact
his is triggered when a contact is offered to an agent for handling.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**                | **Description**                                                                                                                                                    |
|--------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `ronaTimeout`            | Ring-no-answer timeout, in seconds, for the agent to accept the offered contact before RONA handling is triggered.                                                 |
| `agentEmailId`           | Email address or masked email identifier of the agent receiving the contact offer.                                                                                 |
| `contactAssignmentType`  | Indicates how the contact was assigned to the agent. Example value: `ACD`.                                                                                         |

</details>

```json
{
  "type": "AgentOfferContact",
  "eventType": "RoutingMessage",
  "interactionId": "interaction-id-1",
  "orgId": "org-id-1",
  "queueMgr": "aqm",
  "mediaResourceId": "media-resource-id-1",
  "agentId": "agent-id-1",
  "ronaTimeout": 18,
  "interaction": {...},
  "trackingId": "tracking-id-1",
  "eventTime": 1700000000000,
  "agentEmailId": "a***@example.com",
  "contactAssignmentType": "ACD"
}
```
