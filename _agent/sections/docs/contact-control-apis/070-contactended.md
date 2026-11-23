---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-control-apis
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- ContactEnded
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-control-apis). [Full Markdown](../../../../docs/contact-control-apis.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Registering for Websocket Connection](002-registering-for-websocket-connection.md) [Common Payload Fields](003-common-payload-fields.md)

## Article introduction

---

# Contact Control APIs

When invoking the following Contact Control APIs, it is important to know that they are asynchronous and may return any of the notification payloads in this guide at any point.

## Selected section

## ContactEnded
This is triggered when an active contact ends.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**             | **Description**                                                                                                                                                      |
|-----------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `agentsPendingWrapUp` | List of agents who still have wrap-up work pending after the contact ended, when applicable.                                                                         |
| `terminatingParty`    | Participant that caused the contact to end. Example values: `Agent`, `Customer`, `System`.                                                                           |
| `reason`              | End reason associated with the contact termination. Example values: `Customer Left`, `AGENT_LEFT`, `SYSTEM_ERROR`.                                                   |
| `agentEmailId`        | Agent email identifier associated with the contact, when available.                                                                                                  |

</details>

```json
{
  "type": "ContactEnded",
  "eventType": "RoutingMessage",
  "interactionId": "3b1e9f6a-8c44-4b0e-a2d7-5c6a9f2d1e73",
  "orgId": "7f2c5d91-3a6e-4f89-b2c4-1e8d9a7b6c55",
  "queueMgr": "aqm",
  "mediaResourceId": "9a4d7c12-5b8e-4f3c-a1d9-6e2b7f8c0d44",
  "interaction": {...},
  "trackingId": "c6e1a9b4-2d7f-4c88-9a11-3f5d6e7b8c22",
  "agentsPendingWrapUp": [
    "d2b7f3c8-6e4a-4a91-8c3d-9f2b6e1a7c55"
  ],
  "terminatingParty": "Customer",
  "reason": "Customer Left",
  "eventTime": 1776160552810,
  "agentEmailId": "*************************"
}
```
