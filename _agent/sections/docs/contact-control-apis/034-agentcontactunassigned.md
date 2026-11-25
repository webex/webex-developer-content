---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-control-apis
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- AgentContactUnassigned
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-control-apis). [Full Markdown](../../../../docs/contact-control-apis.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Registering for Websocket Connection](002-registering-for-websocket-connection.md) [Common Payload Fields](003-common-payload-fields.md)

## Article introduction

---

# Contact Control APIs

When invoking the following Contact Control APIs, it is important to know that they are asynchronous and may return any of the notification payloads in this guide at any point.

## Selected section

## AgentContactUnassigned
This is triggered when a contact is unassigned from an agent during routing or transfer handling.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**         | **Description**                                                                                                                                            |
|-------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `reason`          | Optional reason returned for the unassignment event.                                                                                                       |
| `reasonCode`      | Optional numeric code associated with the reason.                                                                                                          |

</details>

```json
{
  "type": "AgentContactUnassigned",
  "eventType": "RoutingMessage",
  "interactionId": "542f0d71-ca8d-4cc6-82e6-9e8fa913dc11",
  "orgId": "d93976e7-d3f0-45d2-b885-e7db5dfb98d6",
  "queueMgr": "queue-manager",
  "mediaResourceId": "2517a2ec-742e-4890-8c7f-42232ff05974",
  "agentId": "89d4d02f-b481-4606-a273-2ecc7cdd9439",
  "interaction": {...},
  "trackingId": "c9753b26-f9ce-4f5f-9d6e-bb97598980a6",
  "reason": null,
  "reasonCode": null,
  "eventTime": 1700000010000
}
```
