---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-control-apis
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- AgentStateChangeSuccess
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-control-apis). [Full Markdown](../../../../docs/contact-control-apis.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Registering for Websocket Connection](002-registering-for-websocket-connection.md) [Common Payload Fields](003-common-payload-fields.md)

## Article introduction

---

# Contact Control APIs

When invoking the following Contact Control APIs, it is important to know that they are asynchronous and may return any of the notification payloads in this guide at any point.

## Selected section

## AgentStateChangeSuccess
This is triggered when an agent state change request is successfully applied.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**                     | **Description**                                                                                                      |
|-------------------------------|----------------------------------------------------------------------------------------------------------------------|
| `status`                      | Agent status after the state change. Example value: `LoggedIn`.                                                      |
| `subStatus`                   | Agent sub-status after the state change. Example values: `Idle`, `Available`.                                        |
| `auxCodeId`                   | Auxiliary code identifier associated with the updated sub-status.                                                    |
| `lastStateChangeTimestamp`    | Timestamp (epoch milliseconds) when the state was last changed.                                                      |
| `lastStateChangeReason`       | Reason text associated with the state change operation.                                                              |
| `lastIdleCodeChangeTimestamp` | Timestamp (epoch milliseconds) when the idle/aux code was last changed, if available.                                |
| `connectedChannels`           | Connected channel identifiers for the agent session.                                                                 |
| `changedById`                 | Unique Identifier of the user who initiated the state change, if available.                                          |
| `changedBy`                   | Source or actor that initiated the state change, if available. Example values: `SELF`, `SUPERVISOR`, `HELPDESK` etc. |
| `changedByName`               | Name of the user who initiated the state change, if available.                                                       |

</details>

```json
{
  "eventType": "AgentDesktopMessage",
  "type": "AgentStateChangeSuccess",
  "agentId": "aa0fb53e-736b-4be2-941d-24799292591b",
  "orgId": "689d8edf-3e5d-4e50-be99-59694b10ddde",
  "status": "LoggedIn",
  "subStatus": "Idle",
  "auxCodeId": "866eca53-d884-404a-b080-1ba336473d60",
  "agentSessionId": "1b6b84d0-ecba-45a5-94eb-2b22097b081d",
  "trackingId": "da62c8e1-baa8-45b7-8de9-65cc03987a7e",
  "lastStateChangeTimestamp": 1774349599073,
  "lastStateChangeReason": "",
  "lastIdleCodeChangeTimestamp": 1774349599073,
  "connectedChannels": [],
  "changedById": "aa0fb53e-736b-4be2-941d-24799292591b",
  "changedBy": "SELF",
  "changedByName": "************",
  "eventTime": 1774349599078
}
```
