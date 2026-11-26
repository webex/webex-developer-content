---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-control-apis
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- AgentInviteFailed
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-control-apis). [Full Markdown](../../../../docs/contact-control-apis.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Registering for Websocket Connection](002-registering-for-websocket-connection.md) [Common Payload Fields](003-common-payload-fields.md)

## Article introduction

---

# Contact Control APIs

When invoking the following Contact Control APIs, it is important to know that they are asynchronous and may return any of the notification payloads in this guide at any point.

## Selected section

## AgentInviteFailed
This is triggered when an attempt to invite an agent fails.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**        | **Description**                                                                                                                                 |
|------------------|-------------------------------------------------------------------------------------------------------------------------------------------------|
| `reason`         | Failure reason returned on why the invite failed.                                                                                               |
| `reasonCode`     | Numeric code associated with the failure reason.                                                                                                |
| `agentType`      | Type/category of the invited agent.                                                                                                             |

</details>

```json
{
  "type": "AgentInviteFailed",
  "eventType": "RoutingMessage",
  "interactionId": "4e7d2c91-8f3b-4c5a-9a61-2b8d7e1c6f40",
  "orgId": "9b6f2a4d-3c8e-4a71-b5d9-0f1e7c8a2643",
  "queueMgr": "dummy_qm",
  "agentId": "2a6c8f5e-4b91-4d73-9e20-7c3b1d5a648f",
  "interaction": {...},
  "reason": "DUMMY_REASON",
  "reasonCode": 0,
  "trackingId": "3f7b9d2e-6c4a-4f51-8e90-1a2c5b6d7f48",
  "agentType": "Dummy",
  "eventTime": 0,
  "agentSessionId": "8c5a7d2f-4e91-4b63-9f20-1d6e3a9c748b"
}
```
