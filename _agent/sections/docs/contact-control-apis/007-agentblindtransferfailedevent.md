---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-control-apis
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- AgentBlindTransferFailedEvent
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-control-apis). [Full Markdown](../../../../docs/contact-control-apis.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Registering for Websocket Connection](002-registering-for-websocket-connection.md) [Common Payload Fields](003-common-payload-fields.md)

## Article introduction

---

# Contact Control APIs

When invoking the following Contact Control APIs, it is important to know that they are asynchronous and may return any of the notification payloads in this guide at any point.

## Selected section

## AgentBlindTransferFailedEvent
This is triggered when a blind transfer fails.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**         | **Description**                                                                                               |
|-------------------|---------------------------------------------------------------------------------------------------------------|
| `destAgentId`     | Unique identifier of the destination agent to whom the blind transfer was attempted.                          |
| `reason`          | Failure reason returned on why the blind transfer failed. Example values:`CONTACT_NOT_FOUND`                  |
| `reasonCode`      | Numeric code associated with the failure reason. Example values:`1042` (CONTACT_NOT_FOUND).                   |
| `destinationType` | Type of the transfer destination. Example values:`Agent`,`DN`,`EP-DN`.                                        |

</details>

```json
{
  "eventType": "RoutingMessage",
  "interactionId": "cfaac3d5-8e1a-4fc4-80a0-3d604f273987",
  "orgId": "73081463-94b9-4ace-bc6f-d597d1354bf1",
  "agentId": "7faa3405-cf82-4397-b64d-5bfee23ffc55",
  "destAgentId": "1ac430d9-70bd-4e89-97f8-a799d1572a87",
  "agentSessionId": "208b965f-4a7a-4f54-84c6-18bc838ad37d",
  "trackingId": "96ce9730-14e2-11ee-b8fa-537f253a2f1a",
  "reason": "CONTACT_NOT_FOUND",
  "reasonCode": 1042,
  "destinationType": "Agent",
  "eventTime": 1687867392081,
  "type": "AgentBlindTransferFailedEvent"
}
```
