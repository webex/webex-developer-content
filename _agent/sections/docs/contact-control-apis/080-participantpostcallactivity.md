---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-control-apis
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- ParticipantPostCallActivity
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-control-apis). [Full Markdown](../../../../docs/contact-control-apis.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Registering for Websocket Connection](002-registering-for-websocket-connection.md) [Common Payload Fields](003-common-payload-fields.md)

## Article introduction

---

# Contact Control APIs

When invoking the following Contact Control APIs, it is important to know that they are asynchronous and may return any of the notification payloads in this guide at any point.

## Selected section

## ParticipantPostCallActivity
This is triggered when post-call activity starts for a participant on the main or consult leg of an interaction, typically after the customer leaves while the interaction or consult leg remains active.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**         | **Description**                                                                                                                            |
|-------------------|--------------------------------------------------------------------------------------------------------------------------------------------|
| `participantId`   | Identifier of the participant for whom post-call activity started.                                                                         |
| `participantType` | Type of participant for whom post-call activity started. Example values: `Agent`, `DN`.                                                    |
| `callLegType`     | Indicates whether the post-call activity applies to the main leg or consult leg. Example values: `MAIN_CALL`, `CONSULT`.                   |

</details>

```json
{
  "type": "ParticipantPostCallActivity",
  "eventType": "RoutingMessage",
  "interactionId": "interaction-id-1",
  "orgId": "org-id-1",
  "queueMgr": "queue-manager-1",
  "participantId": "participant-id-1",
  "interaction": {...},
  "trackingId": "tracking-id-1",
  "participantType": "Agent",
  "callLegType": {
    "type": "MAIN_CALL"
  },
  "eventTime": 1700000000000
}
```
