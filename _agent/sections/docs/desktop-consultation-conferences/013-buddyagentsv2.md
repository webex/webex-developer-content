---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-consultation-conferences
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Agent Contact Methods
- buddyAgentsV2()
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/desktop-consultation-conferences). [Full Markdown](../../../../docs/desktop-consultation-conferences.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before You Begin](001-before-you-begin.md)

## Article introduction

Use the Desktop SDK to consult agents and queues and manage conference participants.

## Parent context

## Agent Contact Methods

These methods belong to `Desktop.agentContact`. Use the V2 method where the older method is marked for deprecation.

## Selected section

### buddyAgentsV2()

Fetches the list of agents available for consult call and conference call.

**Example**

```javascript
await Desktop.agentContact.buddyAgentsV2({
    data: {
        agentProfileId: "AXCLfZhH9S1oTdqE1OFw",
        channelName: "chat",
        state: "Available"
    }
});
```

The following table lists the payload details:

| Name              | Type   | Description                             | Required |
| ----------------- | ------ | --------------------------------------- | -------- |
| data              | Object | Options of the buddy agents.            | Yes      |
| -->agentProfileId | String | Unique identifier of the agent profile. | Yes      |
| -->channelName    | String | The media channel type such as chat.    | Yes      |
| -->state          | String | The agent availability status.          | Yes      |

**Returns**
`{Object}` The object with the retrieved data.

**Note:** The `type` parameter value in the response payload depends on the success or failure of the method. If the method is successful, the value is `BuddyAgents`; else, `BuddyAgentsRetrieveFailed`.

**Example Response**

```javascript
BuddyAgentResponse = {
  data: {
    agentId: "7c867aa9-ec768-341a-b767-e5hd6ae7g701",
    agentList: [],
    agentSessionId: "25f31485-f41c-4cca-abe5-e12b80735715",
    eventType: "AgentDesktopMessage",
    orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
    trackingId: "1a2737c0-6704-11eb-9a89-971a3ca976b4",
    type: "BuddyAgents"
  },
  orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
  trackingId: "notifs_49119bed-6dbc-48e6-89fa-9dde8da3fc3e",
  type: "BuddyAgents"
};
```
