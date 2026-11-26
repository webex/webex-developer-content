---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-control-apis
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- AgentContactResumed
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-control-apis). [Full Markdown](../../../../docs/contact-control-apis.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Registering for Websocket Connection](002-registering-for-websocket-connection.md) [Common Payload Fields](003-common-payload-fields.md)

## Article introduction

---

# Contact Control APIs

When invoking the following Contact Control APIs, it is important to know that they are asynchronous and may return any of the notification payloads in this guide at any point.

## Selected section

## AgentContactResumed
This is triggered when a paused contact is successfully assigned again.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**                   | **Description**                                                                                                                                                                                                                                              |
|-----------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `assignedAgentIdBeforePause` | Unique identifier of the agent assigned to the contact before it was paused.                                                                                                                                                                                  |
| `resumedBy.type`            | Identifies who resumed the contact. Supported values are `RESUMED_BY_AGENT`, `RESUMED_BY_SUPERVISOR`, and `RESUMED_BY_SYSTEM`.                                                                                                                                |
| `resumeReason.type`         | Identifies why the contact resumed. Supported values are `RESUME_REASON_MANUAL`, `RESUME_REASON_PAUSE_TIMEOUT`, and `RESUME_REASON_CUSTOMER_REPLY`.                                                                                                           |

</details>

```json
{
  "type": "AgentContactResumed",
  "eventType": "RoutingMessage",
  "interactionId": "fcb4d956-2e50-4ee3-b82d-4a131d196499",
  "orgId": "6f07de7d-c5e8-4ab3-a065-3a5c4c2df07d",
  "interaction": {...},
  "agentId": "90870b5b-d459-4e0b-8e83-fcdd87532598",
  "assignedAgentIdBeforePause": "90870b5b-d459-4e0b-8e83-fcdd87532598",
  "resumedBy": {
    "type": "RESUMED_BY_AGENT"
  },
  "resumeReason": {
    "type": "RESUME_REASON_MANUAL"
  },
  "trackingId": "0f0ba862-a191-49b1-96b8-63409b79c813",
  "eventTime": 1700000000000
}
```
