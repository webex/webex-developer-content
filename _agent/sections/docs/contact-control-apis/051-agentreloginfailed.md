---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-control-apis
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- AgentReloginFailed
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-control-apis). [Full Markdown](../../../../docs/contact-control-apis.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Registering for Websocket Connection](002-registering-for-websocket-connection.md) [Common Payload Fields](003-common-payload-fields.md)

## Article introduction

---

# Contact Control APIs

When invoking the following Contact Control APIs, it is important to know that they are asynchronous and may return any of the notification payloads in this guide at any point.

## Selected section

## AgentReloginFailed
This is triggered when an agent reload/relogin request fails because the current session state cannot be restored, such as when the agent or channel data cannot be fetched, the voice device is not ready, or reload is not allowed for the current session.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**    | **Description**                                                                                                                                                                                                                                          |
|--------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `reason`     | Failure reason returned for the relogin attempt. Example values: `AGENT_NOT_FOUND`, `AGENT_DN_NOT_REGISTERED`, `AGENT_CHANNEL_NOT_FOUND`, `AGENT_NOT_LOGGED_IN`, `INTERNAL_ERROR`.                                                                       |
| `reasonCode` | Numeric code associated with the failure reason. Example values: `1038` (agent not found), `1041` (DN not registered), `1027` (agent channel not found), `1059` (agent not logged in), `1037` (internal error), `36` (generic relogin failure fallback). |

</details>

```json
{
  "eventType": "AgentDesktopMessage",
  "agentId": "5c2f1a7e-5b49-4d3a-9e6c-2f7a1b4c8d93",
  "orgId": "8c2f1a7e-5b49-4d3a-9e6c-2f7a1b4c8d93",
  "reason": "AGENT_NOT_FOUND",
  "reasonCode": 1038,
  "trackingId": "tracking-id-1",
  "eventTime": 1700000000000,
  "type": "AgentReloginFailed"
}
```
