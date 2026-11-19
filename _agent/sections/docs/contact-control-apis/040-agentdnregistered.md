---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-control-apis
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- AgentDNRegistered
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-control-apis). [Full Markdown](../../../../docs/contact-control-apis.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Registering for Websocket Connection](002-registering-for-websocket-connection.md) [Common Payload Fields](003-common-payload-fields.md)

## Article introduction

---

# Contact Control APIs

When invoking the following Contact Control APIs, it is important to know that they are asynchronous and may return any of the notification payloads in this guide at any point.

## Selected section

## AgentDNRegistered
This is triggered when an agent's dial number (DN) is successfully registered for contact handling.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**     | **Description**                                                                   |
|---------------|-----------------------------------------------------------------------------------|
| `dn`          | Dial number that was registered for the agent.                                    |
| `isExtension` | Indicates whether the registered DN is an extension.                              |
| `mediaMgr`    | Media manager that processed the DN registration. Example values: `vmm`,`callmm`. |

</details>

```json
{
  "type": "AgentDNRegistered",
  "eventType": "RoutingMessage",
  "agentId": "8fadc403-9ab3-4722-a30e-9cab5f295587",
  "orgId": "1e00dd80-24ab-4bf1-aaf0-06db94af683f",
  "dn": "555***5074",
  "trackingId": "ad8c4597-11b1-44c3-9e0d-ada919720f5f",
  "isExtension": false,
  "mediaMgr": "vmm",
  "eventTime": 1768998476190
}
```
