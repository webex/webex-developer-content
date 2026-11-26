---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-control-apis
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- AgentLogoutSuccess
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-control-apis). [Full Markdown](../../../../docs/contact-control-apis.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Registering for Websocket Connection](002-registering-for-websocket-connection.md) [Common Payload Fields](003-common-payload-fields.md)

## Article introduction

---

# Contact Control APIs

When invoking the following Contact Control APIs, it is important to know that they are asynchronous and may return any of the notification payloads in this guide at any point.

## Selected section

## AgentLogoutSuccess
This is triggered when an agent logout request is successfully completed and the session is closed.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**         | **Description**                                                                   |
|-------------------|-----------------------------------------------------------------------------------|
| `status`          | Agent status after logout (for example, `LoggedOut`).                             |
| `subStatus`       | Agent sub-status at logout completion (for example, `Idle`).                      |
| `loggedOutBy`     | Actor that initiated the logout. Example values: `MACHINE`, `SELF`, `SUPERVISOR`. |
| `roles`           | Roles associated with the user for this logout event.                             |
| `logoutReason`    | Logout reason.                                                                    |
| `wrapupAuxCodeId` | Wrap-up auxiliary code identifier associated with logout, when available.         |
</details>

```json
{
  "eventType": "AgentDesktopMessage",
  "type": "AgentLogoutSuccess",
  "agentId": "5c6f12a9-39ce-4867-9031-1123783d4ca1",
  "orgId": "84ff943d-11b3-4a4f-9fa1-ec75bc0be2e7",
  "status": "LoggedOut",
  "subStatus": "Idle",
  "agentSessionId": "b2ed5c84-cd20-4fe5-8063-b7f14020dedb",
  "loggedOutBy": "SELF",
  "trackingId": "d70f305c-4f51-4315-ad81-13bddfb99ace",
  "roles": ["agent"],
  "logoutReason": "Agent Logged Out",
  "wrapupAuxCodeId": null,
  "eventTime": 1774336757816
}
```
