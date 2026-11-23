---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-control-apis
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- ContactRecordingStarted
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-control-apis). [Full Markdown](../../../../docs/contact-control-apis.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Registering for Websocket Connection](002-registering-for-websocket-connection.md) [Common Payload Fields](003-common-payload-fields.md)

## Article introduction

---

# Contact Control APIs

When invoking the following Contact Control APIs, it is important to know that they are asynchronous and may return any of the notification payloads in this guide at any point.

## Selected section

## ContactRecordingStarted
This is triggered when contact recording is successfully started for an interaction.

For field details, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

```json
{
  "type": "ContactRecordingStarted",
  "eventType": "RoutingMessage",
  "interactionId": "c3b7a9e2-4f1d-4a83-9c50-2e8d1f6b2041",
  "orgId": "a6d9c4b7-3e2f-4a81-9b50-1e7c5d8a2042",
  "queueMgr": "dummy_qm",
  "interaction": {...},
  "trackingId": "f7a2c9d1-6b3e-4a83-9c50-1e6d7b2a2050",
  "eventTime": 1768911903735
}
```
