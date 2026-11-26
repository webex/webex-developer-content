---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-control-apis
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- CampaignAgentReserved
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-control-apis). [Full Markdown](../../../../docs/contact-control-apis.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Registering for Websocket Connection](002-registering-for-websocket-connection.md) [Common Payload Fields](003-common-payload-fields.md)

## Article introduction

---

# Contact Control APIs

When invoking the following Contact Control APIs, it is important to know that they are asynchronous and may return any of the notification payloads in this guide at any point.

## Selected section

## CampaignAgentReserved
This is triggered when an agent is successfully reserved to handle a campaign call.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**                     | **Description**                                                                                                                                   |
|-------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------|
| `campaignId`                  | Unique identifier of the dialer campaign.                                                                                                         |
| `agentChannelId`              | Unique identifier for the channel associated with this agent and campaign.                                                                        |
| `mediaType`                   | Type of media in used on this campaign.                                                                                                           |

</details>

```json
{
  "eventType": "AgentDesktopMessage",
  "orgId": "org-id-1",
  "campaignId": "campaign-id-1",
  "agentId": "agent-id-1",
  "agentSessionId": "agent-session-id-1",
  "agentChannelId": "agent-channel-id-1",
  "mediaType": "telephony",
  "queueId": "queue-id-1",
  "trackingId": "tracking-id-1",
  "eventTime": 1700000000000,
  "type": "CampaignAgentReserved"
}
```
