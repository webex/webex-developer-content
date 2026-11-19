---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-control-apis
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- AgentOutboundFailed
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-control-apis). [Full Markdown](../../../../docs/contact-control-apis.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Registering for Websocket Connection](002-registering-for-websocket-connection.md) [Common Payload Fields](003-common-payload-fields.md)

## Article introduction

---

# Contact Control APIs

When invoking the following Contact Control APIs, it is important to know that they are asynchronous and may return any of the notification payloads in this guide at any point.

## Selected section

## AgentOutboundFailed
This is triggered when an outbound call attempt from an agent fails.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**       | **Description**                                                                                                                                            |
|-----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `mediaType`     | Media channel of the interaction. Example value: `telephony`.                                                                                              |
| `reason`        | Failure reason returned for the outbound attempt. Example value: `AGENT_ENDS`.                                                                             |
| `reasonCode`    | Numeric code associated with the failure reason. Example value: `1024`.                                                                                    |

</details>

```json
{
  "type": "AgentOutboundFailed",
  "eventType": "RoutingMessage",
  "interactionId": "8c2f1a7e-5b49-4d3a-9e6c-3f7a1b4c8d93",
  "orgId": "8c2f1a7e-5b49-4d3a-9e6c-2f7a1b4c8d93",
  "agentId": "5c2f1a7e-5b49-4d3a-9e6c-2f7a1b4c8d93",
  "mediaType": "telephony",
  "queueId": "queue-id-1",
  "queueMgr": "aqm",
  "reason": "AGENT_ENDS",
  "reasonCode": 1024,
  "interaction": {...},
  "trackingId": "8c2f1a7e-6b49-4d3a-9e6c-2f7a1b4c8d93",
  "eventTime": 1700000000000
}
```
