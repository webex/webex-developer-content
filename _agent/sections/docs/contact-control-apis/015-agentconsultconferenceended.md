---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-control-apis
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- AgentConsultConferenceEnded
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-control-apis). [Full Markdown](../../../../docs/contact-control-apis.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Registering for Websocket Connection](002-registering-for-websocket-connection.md) [Common Payload Fields](003-common-payload-fields.md)

## Article introduction

---

# Contact Control APIs

When invoking the following Contact Control APIs, it is important to know that they are asynchronous and may return any of the notification payloads in this guide at any point.

## Selected section

## AgentConsultConferenceEnded
This is triggered when a consult conference ends successfully.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**                | **Description**                                                                                                                     |
|--------------------------|-------------------------------------------------------------------------------------------------------------------------------------|
| `consultMediaResourceId` | Media resource identifier associated with the consult leg that exited or ended from the conference.                                 |
| `destAgentId`            | Unique identifier of the consult participant associated with the conference end event. In the example, this is an agent identifier. |
| `destinationType`        | Type of the conference participant destination. Example values:`Agent`,`DN`,`EP-DN`.                                                |
| `force`                  | Boolean flag indicating whether the conference exit/end was forced. Example values:`false`,`true`.                                  |

</details>

```json
{
  "type": "AgentConsultConferenceEnded",
  "eventType": "RoutingMessage",
  "interactionId": "d9164514-aaab-4220-bbfd-457ff844e279",
  "orgId": "d5284d60-7175-4700-a692-9d861ad3d589",
  "queueMgr": "dummy-queue-manager",
  "consultMediaResourceId": "consult_CSRVZRQN2T4KZ2KB",
  "agentId": "29d67c88-751b-40fb-9672-34f73549c89e",
  "destAgentId": "e98147f3-9f1b-4baf-9062-96584ba31766",
  "interaction": {...},
  "trackingId": "7d5259bb-c3f7-468d-8d72-a7dfa3458e72",
  "destinationType": "Agent",
  "force": false,
  "eventTime": 1687870870115
}
```
