---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-control-apis
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- ContactCallbackFailed
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-control-apis). [Full Markdown](../../../../docs/contact-control-apis.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Registering for Websocket Connection](002-registering-for-websocket-connection.md) [Common Payload Fields](003-common-payload-fields.md)

## Article introduction

---

# Contact Control APIs

When invoking the following Contact Control APIs, it is important to know that they are asynchronous and may return any of the notification payloads in this guide at any point.

## Selected section

## ContactCallbackFailed
This is triggered when a callback attempt for a contact fails.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**          | **Description**                                                                         |
|--------------------|-----------------------------------------------------------------------------------------|
| `terminatingParty` | Entity that caused the callback attempt to terminate. Example values: `Agent`.          |
| `reason`           | Failure reason returned on why the callback failed. Example values: `AGENT_ENDS`.       |
| `reasonCode`       | Numeric code associated with the failure reason. Example values: `1000` (`AGENT_ENDS`). |

</details>

```json
{
  "type": "ContactCallbackFailed",
  "eventType": "RoutingMessage",
  "interactionId": "interaction-id-1",
  "orgId": "org-id-1",
  "queueMgr": "queue-manager-1",
  "agentId": "agent-id-1",
  "queueId": "queue-id-1",
  "terminatingParty": "Agent",
  "reason": "AGENT_ENDS",
  "reasonCode": 1000,
  "interaction": {...},
  "trackingId": "tracking-id-1",
  "eventTime": 1700000000000
}
```
