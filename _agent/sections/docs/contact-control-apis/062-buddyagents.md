---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-control-apis
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- BuddyAgents
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-control-apis). [Full Markdown](../../../../docs/contact-control-apis.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Registering for Websocket Connection](002-registering-for-websocket-connection.md) [Common Payload Fields](003-common-payload-fields.md)

## Article introduction

---

# Contact Control APIs

When invoking the following Contact Control APIs, it is important to know that they are asynchronous and may return any of the notification payloads in this guide at any point.

## Selected section

## BuddyAgents
This is triggered when a Buddy Agents List request is successfully processed and the matching buddy agent list is returned.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**               | **Description**                                                             |
|-------------------------|-----------------------------------------------------------------------------|
| `agentList`             | List of buddy agents that match the request filters (team/state/channel).   |
| `agentList[].agentId`   | Unique identifier of the buddy agent.                                       |
| `agentList[].agentName` | Display name of the buddy agent.                                            |
| `agentList[].siteId`    | Site identifier associated with the buddy agent.                            |
| `agentList[].teamId`    | Team identifier associated with the buddy agent.                            |
| `agentList[].dn`        | Buddy agent dial number (when available).                                   |
| `agentList[].state`     | Current state shown for the buddy agent (for example, `Available`, `Idle`). |

</details>

```json
{
  "eventType": "AgentDesktopMessage",
  "agentId": "59195cc8-6e7a-41bf-af7f-b60ca8395225",
  "orgId": "bde75a64-f4d5-4ffc-a239-feb607c17ef8",
  "trackingId": "f82cd0a2-973d-4cd3-9e86-01a3a2410cd7",
  "agentList": [
    {
      "agentId": "59195cc8-6e7a-41bf-af7f-b60ca8395225",
      "agentName": "digitalmm-e2e-user1 d",
      "siteId": "96c8ddab-29da-4ff2-a701-bc28c9f52f76",
      "teamId": "59ce6eba-d6b7-4bdc-b38d-8b17eafa4458",
      "dn": "55163",
      "state": "Available"
    }
  ],
  "agentSessionId": "5b6679ad-064b-49f0-a647-9fdd2b978735",
  "type": "BuddyAgents"
}
```
