---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-control-apis
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- AgentBlindTransferred
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-control-apis). [Full Markdown](../../../../docs/contact-control-apis.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Registering for Websocket Connection](002-registering-for-websocket-connection.md) [Common Payload Fields](003-common-payload-fields.md)

## Article introduction

---

# Contact Control APIs

When invoking the following Contact Control APIs, it is important to know that they are asynchronous and may return any of the notification payloads in this guide at any point.

## Selected section

## AgentBlindTransferred
This is triggered when a blind transfer to another participant is successful.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**         | **Description**                                                                                                                                            |
|-------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `destAgentId`     | Unique identifier of the destination agent to whom the contact was blind transferred.                                                                      |
| `destinationType` | Type of the transfer destination. Example vales: `Agent`,`DN`,`EP-DN`.                                                                                      |

</details>

```json
{
  "type": "AgentBlindTransferred",
  "eventType": "RoutingMessage",
  "interactionId": "0fa1d0dd-9ece-48a3-a7dd-80dd12730444",
  "orgId": "2f342cf9-178b-46d1-ba54-35adda6e36d2",
  "queueMgr": "dummy-queue-manager",
  "mediaResourceId": "0fa1d0dd-9ece-48a3-a7dd-80dd12730444",
  "agentId": "001e9881-c04c-4a70-bace-1445f750b71c",
  "destAgentId": "54f0d7e3-938e-4b59-8be8-b0e40fb43b36",
  "interaction": {...},
  "destinationType": "Agent",
  "trackingId": "ed55a956-1d97-43d8-a309-4686166e3af9"
}
```
