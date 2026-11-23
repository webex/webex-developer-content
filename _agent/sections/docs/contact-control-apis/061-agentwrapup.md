---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-control-apis
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- AgentWrapup
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-control-apis). [Full Markdown](../../../../docs/contact-control-apis.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Registering for Websocket Connection](002-registering-for-websocket-connection.md) [Common Payload Fields](003-common-payload-fields.md)

## Article introduction

---

# Contact Control APIs

When invoking the following Contact Control APIs, it is important to know that they are asynchronous and may return any of the notification payloads in this guide at any point.

## Selected section

## AgentWrapup
This is triggered when an agent is moved into wrap-up for a contact after the contact has ended.

For field details , refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

```json
{
  "type": "AgentWrapup",
  "eventType": "RoutingMessage",
  "interactionId": "5a7c2e91-3f4d-4b8a-9c12-6d8e1f0a7b33",
  "orgId": "8d1b6f3c-2a74-4e90-b5c8-9f3a2d7e6c11",
  "queueMgr": "aqm",
  "mediaResourceId": "c3e9a1b7-6d2f-4c88-a5e1-0b7d9f2c4a55",
  "agentId": "1f8c7a2d-9b3e-4d11-a6c4-5e2f7b9d8a66",
  "interaction": {...},
  "trackingId": "7b2d4e9c-1a6f-4c33-8d5e-2f9a7b6c1d88",
  "queueId": "e4c1a9d7-5b3f-4a66-9c21-8d7e2f1b0a44",
  "eventTime": 1776165847699
}
```
