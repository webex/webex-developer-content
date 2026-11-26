---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-control-apis
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- ContactRecordingResumed
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-control-apis). [Full Markdown](../../../../docs/contact-control-apis.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Registering for Websocket Connection](002-registering-for-websocket-connection.md) [Common Payload Fields](003-common-payload-fields.md)

## Article introduction

---

# Contact Control APIs

When invoking the following Contact Control APIs, it is important to know that they are asynchronous and may return any of the notification payloads in this guide at any point.

## Selected section

## ContactRecordingResumed
This is triggered when contact recording is successfully resumed for an active interaction.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**       | **Description**                                                                                                                                            |
|-----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `autoResumed`   | Indicates whether the recording was resumed automatically.                                                                                                 |

</details>

```json
{
  "type": "ContactRecordingResumed",
  "eventType": "RoutingMessage",
  "interactionId": "cdd8f523-d93a-4e7d-910f-1358ac89af35",
  "orgId": "0daafeaf-be86-4363-b7f7-e4adae722cac",
  "queueMgr": "queue-manager",
  "interaction": {...},
  "trackingId": "87008868-1069-4c3c-82b9-eceaa3027314",
  "autoResumed": false,
  "eventTime": 1700000008000
}
```
