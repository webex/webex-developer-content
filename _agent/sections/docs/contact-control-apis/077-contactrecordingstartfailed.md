---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-control-apis
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- ContactRecordingStartFailed
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-control-apis). [Full Markdown](../../../../docs/contact-control-apis.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Registering for Websocket Connection](002-registering-for-websocket-connection.md) [Common Payload Fields](003-common-payload-fields.md)

## Article introduction

---

# Contact Control APIs

When invoking the following Contact Control APIs, it is important to know that they are asynchronous and may return any of the notification payloads in this guide at any point.

## Selected section

## ContactRecordingStartFailed
This is triggered when a request to start contact recording fails.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**    | **Description**                                                                                                    |
|--------------|--------------------------------------------------------------------------------------------------------------------|
| `reason`     | Failure reason returned on why the recording start request failed. Example values: `MEDIA_MANAGER_INTERNAL_ERROR`. |
| `reasonCode` | Numeric code associated with the failure reason. Example values: `100` (`MEDIA_MANAGER_INTERNAL_ERROR`).           |

</details>

```json
{
  "type": "ContactRecordingStartFailed",
  "eventType": "RoutingMessage",
  "interactionId": "interaction-id-1",
  "orgId": "org-id-1",
  "interaction": {...},
  "queueMgr": "queue-manager-1",
  "reason": "MEDIA_MANAGER_INTERNAL_ERROR",
  "reasonCode": 100,
  "trackingId": "tracking-id-1",
  "eventTime": 1700000000000
}
```
