---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-control-apis
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- AgentContactAssigned
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-control-apis). [Full Markdown](../../../../docs/contact-control-apis.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Registering for Websocket Connection](002-registering-for-websocket-connection.md) [Common Payload Fields](003-common-payload-fields.md)

## Article introduction

---

# Contact Control APIs

When invoking the following Contact Control APIs, it is important to know that they are asynchronous and may return any of the notification payloads in this guide at any point.

## Selected section

## AgentContactAssigned
This is triggered when a contact is successfully assigned to an agent and is ready to be handled, across both inbound and outbound interaction flows.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**                  | **Description**                                                                                                                                                     |
|----------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `reservationInteractionId` | Optional reservation interaction identifier for campaign/reservation flows.                                                                                         |
| `campaignReservationKey`   | Optional campaign reservation key for outbound campaign flows.                                                                                                      |
| `agentEmailId`             | Optional agent email identifier when available.                                                                                                                     |

</details>

```json
{
  "type": "AgentContactAssigned",
  "eventType": "RoutingMessage",
  "interactionId": "a8814c56-4ad6-46e3-97a7-b073e51158dc",
  "orgId": "4594f7c7-a526-4be6-b6f1-1c752ea75917",
  "queueMgr": "queue-manager",
  "mediaResourceId": "a18e6b3a-e0c1-4bc3-8d38-c1cf9dc33acd",
  "agentId": "343fac6e-bb8a-4c3e-9c94-92201af01f20",
  "interaction": {...},
  "trackingId": "11cc09b9-cecb-4063-b3ac-eb2f762341b9",
  "eventTime": 1700000000000,
  "reservationInteractionId": null,
  "campaignReservationKey": null,
  "agentEmailId": "agent@example.com"
}
```
