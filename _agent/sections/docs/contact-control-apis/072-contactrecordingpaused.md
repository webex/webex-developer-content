---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-control-apis
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- ContactRecordingPaused
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-control-apis). [Full Markdown](../../../../docs/contact-control-apis.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Registering for Websocket Connection](002-registering-for-websocket-connection.md) [Common Payload Fields](003-common-payload-fields.md)

## Article introduction

---

# Contact Control APIs

When invoking the following Contact Control APIs, it is important to know that they are asynchronous and may return any of the notification payloads in this guide at any point.

## Selected section

## ContactRecordingPaused
This is triggered when contact recording is successfully paused for an active interaction.

For field details, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

```json
{
  "type": "ContactRecordingPaused",
  "eventType": "RoutingMessage",
  "interactionId": "1769efd7-229b-4544-b142-ffefcf4acc1e",
  "orgId": "d6897f60-25a7-43fa-9334-e83e0b101974",
  "queueMgr": "queue-manager",
  "interaction": {...},
  "trackingId": "76fd02e4-0cdf-4762-998a-24ca48283c8b",
  "eventTime": 1700000006000
}
```
