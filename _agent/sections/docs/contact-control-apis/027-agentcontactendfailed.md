---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-control-apis
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- AgentContactEndFailed
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-control-apis). [Full Markdown](../../../../docs/contact-control-apis.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Registering for Websocket Connection](002-registering-for-websocket-connection.md) [Common Payload Fields](003-common-payload-fields.md)

## Article introduction

---

# Contact Control APIs

When invoking the following Contact Control APIs, it is important to know that they are asynchronous and may return any of the notification payloads in this guide at any point.

## Selected section

## AgentContactEndFailed
This is triggered when an attempt to end the contact fails.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**         | **Description**                                                                                                                                            |
|-------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `reason`          | Failure reason returned on why the contact end attempt failed. Example values: `INVALID_CHAT_STATUS`.                                                      |
| `reasonCode`      | Numeric code associated with the failure reason. Example values: `150`(INVALID_CHAT_STATUS).                                                               |

</details>

```json
{
  "type": "AgentContactEndFailed",
  "eventType": "RoutingMessage",
  "interactionId": "7aeefb07-0c79-46bf-9c1b-d558201855b0",
  "orgId": "b333ee78-8263-4370-a60a-967182fc91e4",
  "queueMgr": "dummy-queue-manager",
  "mediaResourceId": "CSR0X8VPA0O3PDXX",
  "agentId": "0bf99cb3-faa8-4f3f-abd4-a171776c424a",
  "interaction": {...},
  "reason": "INVALID_CHAT_STATUS",
  "reasonCode": 150,
  "trackingId": "0ccd89f2-639f-445c-a987-02dc1515aed6",
  "eventTime": 1687846566263
}
```
