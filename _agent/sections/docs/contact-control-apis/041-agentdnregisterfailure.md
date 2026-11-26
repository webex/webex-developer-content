---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-control-apis
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- AgentDNRegisterFailure
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-control-apis). [Full Markdown](../../../../docs/contact-control-apis.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Registering for Websocket Connection](002-registering-for-websocket-connection.md) [Common Payload Fields](003-common-payload-fields.md)

## Article introduction

---

# Contact Control APIs

When invoking the following Contact Control APIs, it is important to know that they are asynchronous and may return any of the notification payloads in this guide at any point.

## Selected section

## AgentDNRegisterFailure
This is triggered when an agent DN registration request fails.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**    | **Description**                                                                                      |
|--------------|------------------------------------------------------------------------------------------------------|
| `reason`     | Failure reason returned on why the DN registration failed. Example values: `DUPLICATE_LOCATION`.     |
| `reasonCode` | Numeric code associated with the failure reason. Example values: `127` (`DUPLICATE_LOCATION`).       |
| `mediaMgr`   | Media manager that processed the DN registration request. Example values: `vmm`,`callmm`.            |

</details>

```json
{
  "type": "AgentDNRegisterFailure",
  "eventType": "RoutingMessage",
  "agentId": "efd60e0a-51b3-4926-b4c4-bb040b9788f8",
  "orgId": "c0a54e64-768f-4541-b747-eec09e225252",
  "reason": "DUPLICATE_LOCATION",
  "reasonCode": 127,
  "trackingId": "25bffd46-4b67-4a70-85ee-5e8f71ced1ff",
  "mediaMgr": "callmm",
  "eventTime": 1768984253850
}
```
