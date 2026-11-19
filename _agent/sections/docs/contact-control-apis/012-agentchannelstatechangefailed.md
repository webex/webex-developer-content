---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-control-apis
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- AgentChannelStateChangeFailed
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-control-apis). [Full Markdown](../../../../docs/contact-control-apis.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Registering for Websocket Connection](002-registering-for-websocket-connection.md) [Common Payload Fields](003-common-payload-fields.md)

## Article introduction

---

# Contact Control APIs

When invoking the following Contact Control APIs, it is important to know that they are asynchronous and may return any of the notification payloads in this guide at any point.

## Selected section

## AgentChannelStateChangeFailed
This is triggered when a state change request for a specific agent channel type fails.

> This event is applicable for agents using the v2 login and v2 state-change flows.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**     | **Description**                                                                            |
|---------------|--------------------------------------------------------------------------------------------|
| `channelType` | Channel type for which the state change failed. Example values: `telephony`, `chat`, `email`, `social`. |
| `reason`      | Failure reason returned for the channel state change request.                              |
| `reasonCode`  | Numeric code associated with the failure reason.                                           |

</details>

```json
{
  "eventType": "AgentDesktopMessage",
  "agentId": "7b23f5d9-8d3a-4a19-9a24-2f6a3e8d1b55",
  "orgId": "3e8c7a21-5b94-4d6f-9c71-8a2f0e6d4b33",
  "channelType": "telephony",
  "reason": "INVALID_AGENT_STATE",
  "reasonCode": 1001,
  "trackingId": "d5a9f7c4-6e2b-4f18-b8d2-9c3a1e5f7b90",
  "eventTime": 1779295823027,
  "type": "AgentChannelStateChangeFailed"
}
```
