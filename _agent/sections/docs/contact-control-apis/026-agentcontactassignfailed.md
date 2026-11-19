---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-control-apis
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- AgentContactAssignFailed
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-control-apis). [Full Markdown](../../../../docs/contact-control-apis.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Registering for Websocket Connection](002-registering-for-websocket-connection.md) [Common Payload Fields](003-common-payload-fields.md)

## Article introduction

---

# Contact Control APIs

When invoking the following Contact Control APIs, it is important to know that they are asynchronous and may return any of the notification payloads in this guide at any point.

## Selected section

## AgentContactAssignFailed
This is triggered when a contact assignment to an agent fails across inbound or outbound interaction flows.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**                  | **Description**                                                                                                                                                      |
|----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `reason`                   | Failure reason returned for the assignment attempt. Example values: `PARTICIPANT_ADD_FAILED`, `AGENT_ALREADY_FOUND`,`PARTICIPANT_INVITE_TIMEOUT`.                    |
| `reasonCode`               | Numeric code associated with the failure reason. Example values: `1011` (participant add failed), `1012` (agent already found), `1010` (participant invite timeout). |
| `reservationInteractionId` | Optional reservation interaction identifier for campaign/reservation flows.                                                                                          |
| `campaignReservationKey`   | Optional campaign reservation key for outbound campaign flows.                                                                                                       |
| `agentEmailId`             | Optional agent email identifier when available.                                                                                                                      |

</details>

```json
{
  "type": "AgentContactAssignedFailed",
  "eventType": "RoutingMessage",
  "interactionId": "92e61c7b-fa90-448b-ac51-078fea52c39e",
  "orgId": "13241ad0-31f0-4c71-87ad-75a9859b3b7d",
  "queueMgr": "queue-manager",
  "mediaResourceId": "74fb6da2-de46-4f2f-90ec-41f8a63c092f",
  "agentId": "8a3f681a-9c61-4dcf-a14e-69329759a094",
  "interaction": {...},
  "reason": "USER_DECLINED",
  "reasonCode": 156,
  "trackingId": "98377bd0-9d12-4330-8552-163ec9cb46b7",
  "eventTime": 1700000000000,
  "reservationInteractionId": null,
  "campaignReservationKey": null,
  "agentEmailId": "agent@example.com"
}
```
