---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-control-apis
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- AgentStateChangeFailed
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-control-apis). [Full Markdown](../../../../docs/contact-control-apis.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Registering for Websocket Connection](002-registering-for-websocket-connection.md) [Common Payload Fields](003-common-payload-fields.md)

## Article introduction

---

# Contact Control APIs

When invoking the following Contact Control APIs, it is important to know that they are asynchronous and may return any of the notification payloads in this guide at any point.

## Selected section

## AgentStateChangeFailed
This is triggered when an agent state change request fails due to validation, state, or session constraints.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**    | **Description**                                                                                                                                                        |
|--------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `auxCodeId`  | Auxiliary code provided in the state change request.                                                                                                                   |
| `reason`     | Failure reason returned for the state change attempt. Example values: `STATE_CHANGE_DISALLOWED_IN_PENDING_LOGOUT`, `INVALID_STATE_CHANGE_REQUEST`, `AGENT_NOT_FOUND`.  |
| `reasonCode` | Numeric code associated with the failure reason. Example values: `1087` (pending logout restriction), `1074` (invalid state change request), `1038` (agent not found). |

</details>

```json
{
  "eventType": "AgentDesktopMessage",
  "type": "AgentStateChangeFailed",
  "agentId": "6b1f9c3e-4a72-4d8e-b5c1-9f2a7e6c3d41",
  "orgId": "2c9e5a7d-8f41-4b63-a1d9-3e7c2b4f5a68",
  "auxCodeId": "9d3b7f21-6a5c-4e8d-92b1-c4f7a6e2d9b3",
  "reason": "STATE_CHANGE_DISALLOWED_IN_PENDING_LOGOUT",
  "reasonCode": 1087,
  "trackingId": "5e7a1c9d-3b42-4f8a-9d6c-1b2e3f4a5c7d",
  "eventTime": 1774349285638
}
```
