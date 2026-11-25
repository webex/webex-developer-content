---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-control-apis
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- AgentConsultTransferred
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-control-apis). [Full Markdown](../../../../docs/contact-control-apis.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Registering for Websocket Connection](002-registering-for-websocket-connection.md) [Common Payload Fields](003-common-payload-fields.md)

## Article introduction

---

# Contact Control APIs

When invoking the following Contact Control APIs, it is important to know that they are asynchronous and may return any of the notification payloads in this guide at any point.

## Selected section

## AgentConsultTransferred
This is triggered when a consult transfer to another participant is successful.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**                    | **Description**                                                                                                     |
|------------------------------|---------------------------------------------------------------------------------------------------------------------|
| `consultMediaResourceId`     | Media resource identifier associated with the consult leg created during the consult transfer flow.                 |
| `transferredMediaResourceId` | Media resource identifier for the consult leg that becomes the transferred leg after the consult transfer succeeds. |
| `destAgentId`                | Unique identifier of the destination agent to whom the consult transfer was completed.                              |
| `destinationType`            | Type of the transfer destination. Example values: `Agent`,`DN`,`EP-DN`.                                             |

</details>

```json
{
  "type": "AgentConsultTransferred",
  "eventType": "RoutingMessage",
  "interactionId": "93b1212f-9a62-43a4-ac32-a91e544f02c5",
  "orgId": "d5e3a633-13a6-47b1-93cb-fa0dc2cf9717",
  "queueMgr": "dummy-queue-manager",
  "mediaResourceId": "93b1212f-9a62-43a4-ac32-a91e544f02c5",
  "consultMediaResourceId": "e4081e22-03e4-40c5-9c3e-66016b9659bd",
  "transferredMediaResourceId": "e4081e22-03e4-40c5-9c3e-66016b9659bd",
  "agentId": "95c05c44-8c16-425a-9abb-959329291f23",
  "destAgentId": "0cdbef6d-af48-49d2-9167-398917261ca2",
  "interaction": {...},
  "trackingId": "7e992bc6-527b-4667-81dc-38f3ccc45b28",
  "destinationType": "Agent"
}
```
