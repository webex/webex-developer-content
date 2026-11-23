---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-transfers
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Agent Contact Methods
- vTeamList()
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/desktop-transfers). [Full Markdown](../../../../docs/desktop-transfers.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before You Begin](001-before-you-begin.md)

## Article introduction

Transfer interactions to agents, dial numbers, and queues with the Desktop SDK.

## Parent context

## Agent Contact Methods

These methods belong to `Desktop.agentContact`. Use the V2 method where the older method is marked for deprecation.

## Selected section

### vTeamList()

Retrieves a list of vTeams (queues) available for transfer. Instead of transferring your interaction to a particular agent, you can transfer it to an appropriate queue (vTeam).

**Example**

```javascript
await Desktop.agentContact.vteamList({
    data: {
        agentProfileId: "AXCLfZhH9S1oTdqE1OFw",
        agentSessionId: "5a84d32c-691b-4500-b163-d6cdba2a3163",
        channelType: "chat",
        type: "inboundqueue",
        trackingId: "9c9b97e0-4194-11eb-b819-7b8dd50ee0cd",
    }
});
```

**Payload type**

```typescript
type RequestPayload = {
    data: Contact.VTeam
};
```

The following table lists the payload details:

| Name              | Type   | Description                                                       | Required |
| ----------------- | ------ | ----------------------------------------------------------------- | -------- |
| data              | Object | Options of the list of queues available for transfer.             | Yes      |
| -->agentProfileId | String | Unique identifier of the agent profile.                           | Yes      |
| -->agentSessionId | String | Unique identifier of the agent session.                           | Yes      |
| -->channelType    | String | The media channel type such as chat.                              | Yes      |
| -->type           | String | The type of queue list.                                           | Yes      |
| -->trackingId     | String | Unique identifier based on the queue list available for transfer. | Yes      |

**Returns**
`{Object}` The object with the retrieved data.

**Note:** The `type` parameter value in the response payload depends on the success or failure of the method. If the method is successful, the value is `VteamList`; else, `VteamListFailed`.

**Example Response**

```javascript
const vTeamResponse = {
  data: {
    agentSessionId: "5a84d32c-691b-4500-b163-d6cdba2a3163",
    callData: "",
    data: {
      allowConsultToQueue: true,
      vteamList: [
        {
          analyzerId: "AXT3_BAV0G6K4V3p9euK",
          callDistributionGroups: [],
          channelType: "chat",
          id: "7178",
          maxTimeInQueue: 500,
          name: "Chat_Demo",
          routingType: null,
          skillBasedRoutingType: null,
          type: "inboundqueue"
        },
        {
          analyzerId: "AXNSDOdSQJBc-emowhp3",
          callDistributionGroups: [],
          channelType: "chat",
          id: "5900",
          maxTimeInQueue: 500,
          name: "Chat_Automation_Queue",
          routingType: null,
          skillBasedRoutingType: null,
          type: "inboundqueue"
        },
        {
          analyzerId: "AXDiuOLjKin42Ov3QJXN",
          callDistributionGroups: [],
          channelType: "chat",
          id: "3381",
          maxTimeInQueue: 500,
          name: "Dont_delete_Chat_queue",
          routingType: null,
          skillBasedRoutingType: null,
          type: "inboundqueue"
        },
        {
          analyzerId: "AXCZ1Cc0B023QCbPLXpr",
          callDistributionGroups: [],
          channelType: "chat",
          id: "3270",
          maxTimeInQueue: 500,
          name: "Chat_Queue",
          routingType: null,
          skillBasedRoutingType: null,
          type: "inboundqueue"
        }
      ]
    },
    jsMethod: "vteamListChanged"
  },
  orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
  trackingId: "notifs_0e6eff89-165e-46b6-8c85-1aada01dab82",
  type: "VteamList"
};
```
