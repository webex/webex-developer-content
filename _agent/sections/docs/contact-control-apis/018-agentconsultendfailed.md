---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-control-apis
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- AgentConsultEndFailed
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-control-apis). [Full Markdown](../../../../docs/contact-control-apis.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Registering for Websocket Connection](002-registering-for-websocket-connection.md) [Common Payload Fields](003-common-payload-fields.md)

## Article introduction

---

# Contact Control APIs

When invoking the following Contact Control APIs, it is important to know that they are asynchronous and may return any of the notification payloads in this guide at any point.

## Selected section

## AgentConsultEndFailed
This event is triggered when an attempt to end a consult fails.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**                | **Description**                                                                                                                                            |
|--------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `consultMediaResourceId` | Media resource identifier associated with the consult leg that the system attempted to end.                                                                |
| `destAgentId`            | Identifier of the consult destination associated with the consult leg being ended. In the example, this is a DN value.                                     |
| `reason`                 | Failure reason returned on why the consult end attempt failed. Example values: `MEDIA_MANAGER_PRECONDITION_FAILED`.                                        |
| `reasonCode`             | Numeric code associated with the failure reason. Example values: `142` (Bad Request).                                                                      |

</details>

```json
{
  "type": "AgentConsultEndFailed",
  "eventType": "RoutingMessage",
  "interactionId": "dc0704cc-4e17-4b1a-944e-9d5e86f87b84",
  "orgId": "f222e3af-1a53-42ef-9deb-7520034b8a10",
  "queueMgr": "dummy-queue-manager",
  "consultMediaResourceId": "8e7ae556-3f22-4839-b949-4fcadff7c9d5",
  "agentId": "16839506-7c48-4a71-ba1b-d585e5d37607",
  "destAgentId": "9997770103",
  "interaction": {...},
  "reason": "MEDIA_MANAGER_PRECONDITION_FAILED",
  "reasonCode": 142,
  "trackingId": "cbdd4a89-b4ee-429d-a86d-72855f6a03b9"
}
```
