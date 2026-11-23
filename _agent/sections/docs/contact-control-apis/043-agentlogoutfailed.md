---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-control-apis
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- AgentLogoutFailed
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-control-apis). [Full Markdown](../../../../docs/contact-control-apis.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Registering for Websocket Connection](002-registering-for-websocket-connection.md) [Common Payload Fields](003-common-payload-fields.md)

## Article introduction

---

# Contact Control APIs

When invoking the following Contact Control APIs, it is important to know that they are asynchronous and may return any of the notification payloads in this guide at any point.

## Selected section

## AgentLogoutFailed
This is triggered when an agent logout request fails due to validation, state, or session constraints.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**    | **Description**                                                                                                 |
|--------------|-----------------------------------------------------------------------------------------------------------------|
| `reason`     | Failure reason returned for the logout attempt. Example value: `AGENT_HAS_ASSIGNED_CONTACTS`.                   |
| `reasonCode` | Numeric code associated with the failure reason. Example value: `1039` for assigned contacts preventing logout. |

</details>

```json
{
  "eventType": "AgentDesktopMessage",
  "type": "AgentLogoutFailed",
  "agentId": "7b3b351e-c49f-4cf4-93c4-fddc3b6a6e98",
  "orgId": "0670b522-6ffe-48a9-b7a0-9f4d0f5b8644",
  "reason": "AGENT_HAS_ASSIGNED_CONTACTS",
  "reasonCode": 1039,
  "trackingId": "76c64852-79a5-4410-9172-87479b9d9f93",
  "eventTime": 1774343932852
}
```
