---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-control-apis
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- AgentConsultConferencing
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-control-apis). [Full Markdown](../../../../docs/contact-control-apis.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Registering for Websocket Connection](002-registering-for-websocket-connection.md) [Common Payload Fields](003-common-payload-fields.md)

## Article introduction

---

# Contact Control APIs

When invoking the following Contact Control APIs, it is important to know that they are asynchronous and may return any of the notification payloads in this guide at any point.

## Selected section

## AgentConsultConferencing
This is triggered in consult-to-EP-DN conferencing flows when an agent starts conferencing the consult interaction, and the conferencing update is sent for the parent interaction context.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**                    | **Description**                                                                                                                            |
|------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------|
| `conferencedParticipantId`   | Identifier of the participant being added into the conference.                                                                             |
| `conferencedParticipantType` | Type of participant being added into the conference. Example values: `EP-DN`, `AGENT`.                                                     |

</details>

```json
{
  "type": "AgentConsultConferencing",
  "eventType": "RoutingMessage",
  "interactionId": "interaction-id-1",
  "orgId": "org-id-1",
  "agentId": "agent-id-1",
  "queueMgr": "queue-manager-1",
  "mediaResourceId": "media-resource-id-1",
  "interaction": {...},
  "conferencedParticipantId": "consult-party-id-1",
  "conferencedParticipantType": "EP-DN",
  "trackingId": "tracking-id-1",
  "eventTime": 1700000000000
}
```
