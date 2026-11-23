---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-control-apis
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- AgentOfferConsult
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-control-apis). [Full Markdown](../../../../docs/contact-control-apis.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Registering for Websocket Connection](002-registering-for-websocket-connection.md) [Common Payload Fields](003-common-payload-fields.md)

## Article introduction

---

# Contact Control APIs

When invoking the following Contact Control APIs, it is important to know that they are asynchronous and may return any of the notification payloads in this guide at any point.

## Selected section

## AgentOfferConsult
This is triggered when a consult interaction is offered to the target agent.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**               | **Description**                                                                                                                                 |
|-------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------|
| `consultMediaResourceId`| Unique identifier of the consult media resource associated with the consult offer.                                                              |
| `consultingAgentId`     | Unique identifier of the agent who initiated the consult request.                                                                               |
| `ronaTimeout`           | Ring-no-answer timeout configured for the consult offer.                                                                                        |

</details>

```json
{
  "type": "AgentOfferConsult",
  "eventType": "RoutingMessage",
  "interactionId": "f1a6c9e2-4b7d-4e3f-9a82-1d6c8b5e2047",
  "orgId": "a9e5c4b7-2d8f-4c61-9b30-6e1d7a8f2054",
  "queueMgr": "dummy_qm",
  "consultMediaResourceId": "c6b2e9f1-8a4d-4c73-9f50-1e7d5b8a2049",
  "agentId": "d7e4a1c9-5b6f-4a82-9c30-2e8d1f6b2057",
  "consultingAgentId": "e2b8d6a9-7c5f-4e41-9a30-1f5d8c6b2048",
  "ronaTimeout": 0,
  "interaction": {...},
  "trackingId": "9c3d6a1e-8b4f-4a72-9d50-7e2c1b6a9050",
  "eventTime": 0
}
```
