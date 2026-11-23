---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-control-apis
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- AgentVteamTransferFailed
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-control-apis). [Full Markdown](../../../../docs/contact-control-apis.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Registering for Websocket Connection](002-registering-for-websocket-connection.md) [Common Payload Fields](003-common-payload-fields.md)

## Article introduction

---

# Contact Control APIs

When invoking the following Contact Control APIs, it is important to know that they are asynchronous and may return any of the notification payloads in this guide at any point.

## Selected section

## AgentVteamTransferFailed
This is triggered when a transfer to a virtual team fails.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**       | **Description**                                                                                                                                            |
|-----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `vteamId`       | Unique identifier of the virtual team to which the transfer was attempted.                                                                                 |
| `vteamType`     | Type of the virtual team target. In the example, this is `inboundentrypoint`.                                                                              |
| `reason`        | Failure reason returned on why the virtual team transfer failed. Example values: `INVALID_CHAT_STATUS`.                                                    |
| `reasonCode`    | Numeric code associated with the failure reason. Example values: `150` (INVALID_CHAT_STATUS).                                                              |

</details>

```json
{
  "type": "AgentVteamTransferFailed",
  "eventType": "RoutingMessage",
  "interactionId": "b6f4b924-f7eb-467a-99b4-b20ad8f4975d",
  "orgId": "4df9bd96-7288-44a1-9f1c-40e2038d35b0",
  "queueMgr": "dummy-queue-manager",
  "agentId": "b25cddcc-1841-44ca-b60c-ad3eb0eef87d",
  "vteamId": "0d42888a-143b-4097-a095-4e12ba3d58f7",
  "vteamType": "inboundentrypoint",
  "reason": "INVALID_CHAT_STATUS",
  "reasonCode": 150,
  "interaction": {...},
  "trackingId": "6bc331d0-148e-11ee-a59f-75682fa22e5c",
  "eventTime": 1687831242160
}
```
