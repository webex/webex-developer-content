---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-control-apis
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- AgentOfferContactRona
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-control-apis). [Full Markdown](../../../../docs/contact-control-apis.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Registering for Websocket Connection](002-registering-for-websocket-connection.md) [Common Payload Fields](003-common-payload-fields.md)

## Article introduction

---

# Contact Control APIs

When invoking the following Contact Control APIs, it is important to know that they are asynchronous and may return any of the notification payloads in this guide at any point.

## Selected section

## AgentOfferContactRona
This is triggered when a contact offer times out due to RONA and is not accepted by the agent in time.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**         | **Description**                                                                                                                                            |
|-------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `reasonCode`      | Numeric code associated with the RONA reason. Defaults to `121`.                                                                                           |
| `reason`          | Reason returned for the RONA event. Defaults to RONA_TIMER_EXPIRED.                                                                                        |

</details>

```json
{
  "type": "AgentOfferContactRona",
  "eventType": "RoutingMessage",
  "interactionId": "501d28f5-650c-4a15-87d5-31e572800751",
  "orgId": "bfc4707c-0f52-4607-9efd-582152e764e4",
  "queueMgr": "queue-manager",
  "mediaResourceId": "0066462b-ce70-4b13-b856-e793b659e34f",
  "agentId": "8c72b5f8-6af1-4930-8ac2-c416ff4cbb22",
  "interaction": {...},
  "trackingId": "f46d8f6f-d45d-4d8b-b3b8-2f50a8e6bc64",
  "reasonCode": 121,
  "reason": "RONA_TIMER_EXPIRED",
  "eventTime": 1700000005000,
  "agentSessionId": "8ff66b12-917f-455c-a580-2e387b858ca9"
}
```
