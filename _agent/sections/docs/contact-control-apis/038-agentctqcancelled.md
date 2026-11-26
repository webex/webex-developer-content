---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-control-apis
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- AgentCtqCancelled
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-control-apis). [Full Markdown](../../../../docs/contact-control-apis.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Registering for Websocket Connection](002-registering-for-websocket-connection.md) [Common Payload Fields](003-common-payload-fields.md)

## Article introduction

---

# Contact Control APIs

When invoking the following Contact Control APIs, it is important to know that they are asynchronous and may return any of the notification payloads in this guide at any point.

## Selected section

## AgentCtqCancelled
This is triggered when a consult-to-queue request is cancelled successfully.

For field details, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

```json
{
  "type": "AgentCtqCancelled",
  "eventType": "RoutingMessage",
  "interactionId": "1f1ccfde-58a9-4f8f-8f8c-d12cd1ac3319",
  "orgId": "bde75a64-f4d5-4ffc-a239-feb607c17ef8",
  "queueMgr": "dummy-queue-manager",
  "agentId": "109332be-7fc4-4d4d-9488-ebdb8e13b9bb",
  "queueId": "7c4ac9cf-014d-4e09-9e1f-d26b13704fdc",
  "interaction": {...},
  "trackingId": "f82cd0a2-973d-4cd3-9e86-01a3a2410cd7"
}
```
