---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-control-apis
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- AgentVteamTransferred
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-control-apis). [Full Markdown](../../../../docs/contact-control-apis.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Registering for Websocket Connection](002-registering-for-websocket-connection.md) [Common Payload Fields](003-common-payload-fields.md)

## Article introduction

---

# Contact Control APIs

When invoking the following Contact Control APIs, it is important to know that they are asynchronous and may return any of the notification payloads in this guide at any point.

## Selected section

## AgentVteamTransferred
This is triggered when a transfer to a virtual team is successful.

For field details, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

```json
{
  "type": "AgentVteamTransferred",
  "eventType": "RoutingMessage",
  "interactionId": "29729f46-6f11-40bb-8baa-023e3f9408ed",
  "orgId": "4df9bd96-7288-44a1-9f1c-40e2038d35b0",
  "agentId": "2ea10ee0-fdff-4e98-a98a-96609f0b4fa3",
  "queueMgr": "dummy-queue-manager",
  "interaction": {...},
  "trackingId": "fd10d955-cd2c-401b-a3bb-1de781852a8b",
  "eventTime": 1687869699460
}
```
