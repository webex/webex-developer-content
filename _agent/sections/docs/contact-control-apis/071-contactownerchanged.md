---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-control-apis
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- ContactOwnerChanged
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-control-apis). [Full Markdown](../../../../docs/contact-control-apis.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Registering for Websocket Connection](002-registering-for-websocket-connection.md) [Common Payload Fields](003-common-payload-fields.md)

## Article introduction

---

# Contact Control APIs

When invoking the following Contact Control APIs, it is important to know that they are asynchronous and may return any of the notification payloads in this guide at any point.

## Selected section

## ContactOwnerChanged
This is triggered when contact ownership is transferred from one owner to another—such as during conference participant removal or similar handoff scenarios—and the updated interaction is then routed to the new assigned agent.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**         | **Description**                                                                                                                            |
|-------------------|--------------------------------------------------------------------------------------------------------------------------------------------|
| `fromOwner`       | Identifier of the previous owner of the contact.                                                                                           |
| `toOwner`         | Identifier of the new owner of the contact.                                                                                                |

</details>

```json
{
  "type": "ContactOwnerChanged",
  "eventType": "RoutingMessage",
  "interactionId": "interaction-id-1",
  "orgId": "org-id-1",
  "queueMgr": "queue-manager-1",
  "fromOwner": "agent-id-1",
  "toOwner": "agent-id-2",
  "mediaResourceId": "media-resource-id-1",
  "interaction": {...},
  "trackingId": "tracking-id-1",
  "eventTime": 1700000000000
}
```
