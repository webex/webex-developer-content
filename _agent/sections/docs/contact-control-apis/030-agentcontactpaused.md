---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-control-apis
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- AgentContactPaused
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-control-apis). [Full Markdown](../../../../docs/contact-control-apis.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Registering for Websocket Connection](002-registering-for-websocket-connection.md) [Common Payload Fields](003-common-payload-fields.md)

## Article introduction

---

# Contact Control APIs

When invoking the following Contact Control APIs, it is important to know that they are asynchronous and may return any of the notification payloads in this guide at any point.

## Selected section

## AgentContactPaused
This is triggered when an active non-real-time digital contact is successfully paused by an agent.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

```json
{
  "type": "AgentContactPaused",
  "eventType": "RoutingMessage",
  "interactionId": "fcb4d956-2e50-4ee3-b82d-4a131d196499",
  "orgId": "6f07de7d-c5e8-4ab3-a065-3a5c4c2df07d",
  "interaction": {...},
  "agentId": "90870b5b-d459-4e0b-8e83-fcdd87532598",
  "trackingId": "0f0ba862-a191-49b1-96b8-63409b79c813",
  "eventTime": 1700000000000
}
```
