---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-control-apis
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- AgentContactHoldFailed
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-control-apis). [Full Markdown](../../../../docs/contact-control-apis.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Registering for Websocket Connection](002-registering-for-websocket-connection.md) [Common Payload Fields](003-common-payload-fields.md)

## Article introduction

---

# Contact Control APIs

When invoking the following Contact Control APIs, it is important to know that they are asynchronous and may return any of the notification payloads in this guide at any point.

## Selected section

## AgentContactHoldFailed
This is triggered when an attempt to place an active contact on hold fails.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Description**                                                                                                                                                                 |
|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `reason` - Failure reason returned for the hold attempt. Example values: `USER_LEFT`, `MEDIA_APP_SERVER_ERROR`.                                                                 |
| `reasonCode` - Numeric code associated with the failure reason. Example values: 105 (user left), 138 (media app server error).                                                  |

</details>

```json
{
  "type": "AgentContactHoldFailed",
  "eventType": "RoutingMessage",
  "interactionId": "e7098133-41fb-48ec-8fa1-103f7baef3f8",
  "orgId": "548205a6-bba5-49da-9cfa-c69ea9280fd1",
  "queueMgr": "queue-manager",
  "mediaResourceId": "daa7142b-44b4-453d-a054-0a4d904c9795",
  "agentId": "ce892125-7f8d-467f-b4ef-6b8f9ef7f4b9",
  "interaction": {...},
  "reason": "USER_LEFT",
  "reasonCode": 105,
  "trackingId": "a981de59-a646-4573-8fa7-f2eab7ab6854",
  "eventTime": 1700000000000
}
```
