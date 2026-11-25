---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-control-apis
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- AgentStationLoginFailed
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-control-apis). [Full Markdown](../../../../docs/contact-control-apis.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Registering for Websocket Connection](002-registering-for-websocket-connection.md) [Common Payload Fields](003-common-payload-fields.md)

## Article introduction

---

# Contact Control APIs

When invoking the following Contact Control APIs, it is important to know that they are asynchronous and may return any of the notification payloads in this guide at any point.

## Selected section

## AgentStationLoginFailed
This is triggered when an agent login request fails due to validation, state, or session constraints.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**    | **Description**                                                                                                                                                                     |
|--------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `reason`     | Failure reason returned for the login attempt. Example values: `AGENT_SESSION_ALREADY_EXISTS`, `ALLOWED_AGENT_SESSION_LIMIT_EXCEEDED`, `AGENT_DN_EMPTY`, `DN_REGISTRATION_TIMEOUT`. |
| `reasonCode` | Numeric code associated with the failure reason. Example values: `1035`(session exists) , `1019` (session limit exceded), `1036` (DN empty), `1058` (DN registration timeout).      |
</details>

```json
{
  "eventType": "AgentDesktopMessage",
  "type": "AgentStationLoginFailed",
  "agentId": "7ec529c3-8d13-4f95-a26b-14328517f340",
  "orgId": "9f97820b-d1d1-4e6b-b3eb-983af99aed57",
  "reason": "AGENT_SESSION_ALREADY_EXISTS",
  "reasonCode": 1035,
  "trackingId": "cc59c869-979c-40e9-a59f-93510602e7cc",
  "eventTime": 1774261973099
}
```
