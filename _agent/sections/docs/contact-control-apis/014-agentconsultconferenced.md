---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-control-apis
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- AgentConsultConferenced
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-control-apis). [Full Markdown](../../../../docs/contact-control-apis.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Registering for Websocket Connection](002-registering-for-websocket-connection.md) [Common Payload Fields](003-common-payload-fields.md)

## Article introduction

---

# Contact Control APIs

When invoking the following Contact Control APIs, it is important to know that they are asynchronous and may return any of the notification payloads in this guide at any point.

## Selected section

## AgentConsultConferenced
This is triggered when a consult call is successfully converted to a conference..

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**                | **Description**                                                                                       |
|--------------------------|-------------------------------------------------------------------------------------------------------|
| `consultMediaResourceId` | Media resource identifier associated with the consult leg that was joined into the conference.        |
| `destAgentId`            | Identifier of the consult destination joined into the conference. In the example, this is a DN value. |
| `destinationType`        | Type of the conference destination. Example values: `Agent`,`DN`,`EP-DN`.                             |

</details>

```json
{
  "type": "AgentConsultConferenced",
  "eventType": "RoutingMessage",
  "interactionId": "bc1386ae-ad41-4900-89d1-553fd4010b62",
  "orgId": "bde75a64-f4d5-4ffc-a239-feb607c17ef8",
  "queueMgr": "dummy-queue-manager",
  "mediaResourceId": "bc1386ae-ad41-4900-89d1-553fd4010b62",
  "consultMediaResourceId": "d0bcbd38-881f-4d3f-9c77-67f2f0c5d20c",
  "agentId": "d9090e8b-a35d-46bd-9171-2923acaeefda",
  "destAgentId": "2147651221",
  "interaction": {...},
  "trackingId": "5b6679ad-064b-49f0-a647-9fdd2b978735",
  "destinationType": "DN"
}
```
