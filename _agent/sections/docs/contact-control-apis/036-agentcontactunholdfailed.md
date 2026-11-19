---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-control-apis
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- AgentContactUnHoldFailed
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-control-apis). [Full Markdown](../../../../docs/contact-control-apis.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Registering for Websocket Connection](002-registering-for-websocket-connection.md) [Common Payload Fields](003-common-payload-fields.md)

## Article introduction

---

# Contact Control APIs

When invoking the following Contact Control APIs, it is important to know that they are asynchronous and may return any of the notification payloads in this guide at any point.

## Selected section

## AgentContactUnHoldFailed
This is triggered when an attempt to unhold a contact fails.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**         | **Description**                                                                                                                                            |
|-------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `reason`          | Failure reason returned for the unhold attempt. Example values: `USER_LEFT`.                                                                               |
| `reasonCode`      | Numeric code associated with the failure reason. Example values: 105 (user left).                                                                          |

</details>

```json
{
  "type": "AgentContactUnHoldFailed",
  "eventType": "RoutingMessage",
  "interactionId": "47162758-76dc-4b21-ad45-548547d64f2c",
  "orgId": "0c8ea9ac-8882-42e0-b9d2-06e74009d08b",
  "queueMgr": "queue-manager",
  "mediaResourceId": "110c821c-5ecf-4f8d-ac9c-c55cdc12494a",
  "agentId": "d1e9cf5d-c473-4d0b-82f8-2f779aca0b0e",
  "interaction": {...},
  "reason": "USER_LEFT",
  "reasonCode": 105,
  "trackingId": "979f3da9-c55b-448f-a5d5-98b605d5f6d4",
  "eventTime": 1700000004000
}
```
