---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-control-apis
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- AgentConsultCreated
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-control-apis). [Full Markdown](../../../../docs/contact-control-apis.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Registering for Websocket Connection](002-registering-for-websocket-connection.md) [Common Payload Fields](003-common-payload-fields.md)

## Article introduction

---

# Contact Control APIs

When invoking the following Contact Control APIs, it is important to know that they are asynchronous and may return any of the notification payloads in this guide at any point.

## Selected section

## AgentConsultCreated
This is triggered when a consult interaction is created successfully.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**                | **Description**                                                                                                                                            |
|--------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `consultMediaResourceId` | Media resource identifier associated with the newly created consult leg.                                                                                   |
| `destAgentId`            | Unique identifier of the intended consult destination. In the example, this is another agent identifier.                                                   |
| `destinationType`        | Type of the consult destination. Example values: `Agent`,`DN`,`EP-DN`.                                                                                      |

</details>

```json
{
  "type": "AgentConsultCreated",
  "eventType": "RoutingMessage",
  "interactionId": "6e54dd0f-9da5-4ac6-b56b-a2e3657bbb9f",
  "orgId": "348adfa2-b8f0-405c-a516-da004eefde5f",
  "queueMgr": "dummy-queue-manager",
  "mediaResourceId": "6e54dd0f-9da5-4ac6-b56b-a2e3657bbb9f",
  "consultMediaResourceId": "da957aa2-dfb1-429e-aa5a-a216c874ca38",
  "agentId": "f8373b22-8c29-4e94-8ff6-aa52e50d1a18",
  "destAgentId": "0346a971-acf1-41b0-bb63-c1861e120d30",
  "interaction": {...},
  "trackingId": "c5348bdc-76ff-44c8-9684-7b7a41612656",
  "destinationType": "Agent"
}
```
