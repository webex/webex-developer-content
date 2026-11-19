---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-control-apis
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- CampaignPreviewSkipFailed
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-control-apis). [Full Markdown](../../../../docs/contact-control-apis.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Registering for Websocket Connection](002-registering-for-websocket-connection.md) [Common Payload Fields](003-common-payload-fields.md)

## Article introduction

---

# Contact Control APIs

When invoking the following Contact Control APIs, it is important to know that they are asynchronous and may return any of the notification payloads in this guide at any point.

## Selected section

## CampaignPreviewSkipFailed
This is triggered when a skip action cannot be completed for the agent’s current preview campaign contact.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**       | **Description**                                                                                                                                                      |
|-----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `campaignId`    | Unique identifier of the dialer campaign.                                                                                                                            |
| `reason`        | Failure reason returned for the assignment attempt. Example values: `PARTICIPANT_ADD_FAILED`, `AGENT_ALREADY_FOUND`,`PARTICIPANT_INVITE_TIMEOUT`.                    |
| `reasonCode`    | Numeric code associated with the failure reason. Example values: `1011` (participant add failed), `1012` (agent already found), `1010` (participant invite timeout). |

</details>

```json
{
  "eventType": "AgentDesktopMessage",
  "orgId": "org-id-1",
  "campaignId": "campaign-id-1",
  "agentId": "agent-id-1",
  "interactionId": "interaction-id-1",
  "reason": "INTERNAL_ERROR",
  "reasonCode": 1000,
  "trackingId": "tracking-id-1",
  "eventTime": 1700000000000,
  "type": "CampaignPreviewSkipFailed"
}
```
