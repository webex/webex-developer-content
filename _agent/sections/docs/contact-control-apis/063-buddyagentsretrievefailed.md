---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-control-apis
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- BuddyAgentsRetrieveFailed
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-control-apis). [Full Markdown](../../../../docs/contact-control-apis.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Registering for Websocket Connection](002-registering-for-websocket-connection.md) [Common Payload Fields](003-common-payload-fields.md)

## Article introduction

---

# Contact Control APIs

When invoking the following Contact Control APIs, it is important to know that they are asynchronous and may return any of the notification payloads in this guide at any point.

## Selected section

## BuddyAgentsRetrieveFailed
This is triggered when a Buddy Agents List request fails due to validation, data retrieval, or internal processing constraints.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**    | **Description**                                                                                      |
|--------------|------------------------------------------------------------------------------------------------------|
| `reason`     | Failure reason returned for the buddy list request. Example values: `BUDDY_AGENTS_RETRIEVE_FAILED`.   |
| `reasonCode` | Numeric code associated with the failure reason. Example values: `35` (buddy agents retrieve failed). |

</details>

```json
{
  "eventType": "AgentDesktopMessage",
  "agentId": "59195cc8-6e7a-41bf-af7f-b60ca8395225",
  "orgId": "bde75a64-f4d5-4ffc-a239-feb607c17ef8",
  "trackingId": "f82cd0a2-973d-4cd3-9e86-01a3a2410cd7",
  "reason": "BUDDY_AGENTS_RETRIEVE_FAILED",
  "reasonCode": 35,
  "type": "BuddyAgentsRetrieveFailed"
}
```
