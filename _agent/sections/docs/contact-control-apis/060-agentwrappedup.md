---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-control-apis
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- AgentWrappedUp
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-control-apis). [Full Markdown](../../../../docs/contact-control-apis.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Registering for Websocket Connection](002-registering-for-websocket-connection.md) [Common Payload Fields](003-common-payload-fields.md)

## Article introduction

---

# Contact Control APIs

When invoking the following Contact Control APIs, it is important to know that they are asynchronous and may return any of the notification payloads in this guide at any point.

## Selected section

## AgentWrappedUp
This is triggered when an agent completes wrap-up for a contact and the system records the wrap-up completion.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**         | **Description**                                                                                                                                            |
|-------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `wrapUpAuxCodeId` | Wrap-up code selected when wrap-up was completed, when available.                                                                                          |
| `agentChannelId`  | Agent channel identifier associated with the wrap-up completion, when available.                                                                           |

</details>

```json
{
  "type": "AgentWrappedUp",
  "eventType": "RoutingMessage",
  "interactionId": "88c8f520-fd53-43a2-94fc-7cebf502a361",
  "orgId": "2f342cf9-178b-46d1-ba54-35adda6e36d2",
  "queueMgr": "aqm",
  "agentId": "001e9881-c04c-4a70-bace-1445f750b71c",
  "interaction": {...},
  "trackingId": "3c01a470-2af8-11ed-b83c-0f912c34e136",
  "wrapUpAuxCodeId": "1fd4d25a-c745-4e73-9b44-9be37af6aa72"
}
```
