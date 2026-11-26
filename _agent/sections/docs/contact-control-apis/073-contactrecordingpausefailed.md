---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-control-apis
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- ContactRecordingPauseFailed
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-control-apis). [Full Markdown](../../../../docs/contact-control-apis.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Registering for Websocket Connection](002-registering-for-websocket-connection.md) [Common Payload Fields](003-common-payload-fields.md)

## Article introduction

---

# Contact Control APIs

When invoking the following Contact Control APIs, it is important to know that they are asynchronous and may return any of the notification payloads in this guide at any point.

## Selected section

## ContactRecordingPauseFailed
This is triggered when an attempt to pause contact recording fails.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**       | **Description**                                                                                                                                            |
|-----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `reason`        | Failure reason returned for the pause request. Example values: `MEDIA_MANAGER_INTERNAL_ERROR`.                                                             |
| `reasonCode`    | Numeric code associated with the failure reason. Example values: `136` (media manager error).                                                              |

</details>

```json
{
  "type": "ContactRecordingPauseFailed",
  "eventType": "RoutingMessage",
  "interactionId": "021b02cf-202c-4259-8e49-8eef066f6bce",
  "orgId": "f9a9dd69-1187-4240-8f26-285030e86bf7",
  "queueMgr": "queue-manager",
  "interaction": {...},
  "reason": "UNSUPPORTED_OPERATION_FOR_MEDIATYPE",
  "reasonCode": 162,
  "trackingId": "521ccc55-f94a-4378-93c1-81226134eb80",
  "eventTime": 1700000007000
}
```
