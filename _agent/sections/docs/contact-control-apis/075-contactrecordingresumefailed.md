---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-control-apis
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- ContactRecordingResumeFailed
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-control-apis). [Full Markdown](../../../../docs/contact-control-apis.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Registering for Websocket Connection](002-registering-for-websocket-connection.md) [Common Payload Fields](003-common-payload-fields.md)

## Article introduction

---

# Contact Control APIs

When invoking the following Contact Control APIs, it is important to know that they are asynchronous and may return any of the notification payloads in this guide at any point.

## Selected section

## ContactRecordingResumeFailed
This is triggered when an attempt to resume contact recording fails.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**       | **Description**                                                                                                                                            |
|-----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `reason`        | Failure reason returned for the resume request. Example values: `UNSUPPORTED_OPERATION_FOR_MEDIATYPE`.                                                     |
| `reasonCode`    | Numeric code associated with the failure reason. Example values: `162` (unsupported operation for media type).                                             |

</details>

```json
{
  "type": "ContactRecordingResumeFailed",
  "eventType": "RoutingMessage",
  "interactionId": "f0f71e97-26b6-41f0-8b23-da9c49085858",
  "orgId": "a9cf8d67-59cd-4b69-a397-2221e5fb260c",
  "queueMgr": "queue-manager",
  "interaction": {...},
  "reason": "UNSUPPORTED_OPERATION_FOR_MEDIATYPE",
  "reasonCode": 162,
  "trackingId": "87ede599-f9d9-4ccc-890d-3e43c5c3442f",
  "eventTime": 1700000009000
}
```
