---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-control-apis
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- AgentConferenceTransferred
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-control-apis). [Full Markdown](../../../../docs/contact-control-apis.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Registering for Websocket Connection](002-registering-for-websocket-connection.md) [Common Payload Fields](003-common-payload-fields.md)

## Article introduction

---

# Contact Control APIs

When invoking the following Contact Control APIs, it is important to know that they are asynchronous and may return any of the notification payloads in this guide at any point.

## Selected section

## AgentConferenceTransferred
This is triggered when conference ownership is handed off to a new participant, typically after the primary agent leaves a conference interaction and a new owner is selected.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**           | **Description**                                                                                                                            |
|---------------------|--------------------------------------------------------------------------------------------------------------------------------------------|
| `destAgentId`       | Identifier of the destination participant that became the new conference owner.                                                           |
| `destinationType`   | Type of destination participant that received the conference transfer. Example values: `Agent`, `DN`.                                    |
| `sourceDn`          | Source dial number associated with the transfer, when available.                                                                           |

</details>

```json
{
  "type": "AgentConferenceTransferred",
  "eventType": "RoutingMessage",
  "interactionId": "interaction-id-1",
  "orgId": "org-id-1",
  "queueMgr": "queue-manager-1",
  "mediaResourceId": "media-resource-id-1",
  "agentId": "agent-id-1",
  "destAgentId": "agent-id-2",
  "interaction": {...},
  "trackingId": "tracking-id-1",
  "destinationType": "Agent",
  "sourceDn": "source-dn-1",
  "eventTime": 1700000000000
}
```
