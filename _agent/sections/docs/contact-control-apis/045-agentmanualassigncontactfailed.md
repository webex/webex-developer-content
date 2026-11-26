---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-control-apis
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- AgentManualAssignContactFailed
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-control-apis). [Full Markdown](../../../../docs/contact-control-apis.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Registering for Websocket Connection](002-registering-for-websocket-connection.md) [Common Payload Fields](003-common-payload-fields.md)

## Article introduction

---

# Contact Control APIs

When invoking the following Contact Control APIs, it is important to know that they are asynchronous and may return any of the notification payloads in this guide at any point.

## Selected section

## AgentManualAssignContactFailed
This is triggered when a manual contact assignment request to an agent fails.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**       | **Description**                                                                                                               |
|-----------------|-------------------------------------------------------------------------------------------------------------------------------|
| `reason`        | Failure reason returned on why the manual assignment failed. Example values: `OPERATION_DISALLOWED_FOR_INTERACTION_STATE`.   |
| `reasonCode`    | Numeric code associated with the failure reason. Example values: `1089` (`OPERATION_DISALLOWED_FOR_INTERACTION_STATE`).      |

</details>

```json
{
  "type": "AgentManualAssignContactFailed",
  "eventType": "RoutingMessage",
  "interactionId": "7a4c9e2b-3d6f-4a81-9b50-1e7c5d8a204f",
  "orgId": "c6b8a4e1-9d3f-4b72-8a50-2e7c1d5f904a",
  "agentId": "e9b1c7a4-6d3f-4a82-9c50-7e2d1b5a904b",
  "reason": "OPERATION_DISALLOWED_FOR_INTERACTION_STATE",
  "reasonCode": 1089,
  "trackingId": "2d7c5a9e-4b1f-4e83-9a50-6c8d1b7f904c",
  "eventTime": 1768917624823
}
```
