---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-transfers
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Agent Contact Methods
- blindTransferV2()
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

### blindTransferV2()

Initiates a blind transfer request. This method can be used to transfer a contact to an Agent or to a Dial Number.

#### Blind Transfer to Agent or DialNumber

**Example**

```javascript
await Desktop.agentContact.blindTransferV2({
    interactionId: "08259a2b-bacf-11ea-bdd9-abbd16eaf1d5",
    data: {
        to: "43bfcdef-5551-45b1-a8f9-a0b33e66e3fe",
        destinationType: "agent"
    }
});

await Desktop.agentContact.blindTransferV2({
    interactionId: "08259a2b-bacf-11ea-bdd9-abbd16eaf1d5",
    data: {
        to: "9997770095",
        destinationType: "dialNumber"
    }
});
```

**Payload type**

```typescript
type RequestPayload = {
    interactionId: string;
    data: Contact.blindTransferPayLoad
}

type blindTransferPayLoad = {
    to: string;
    destinationType: string;
};
```

The following table lists the payload details:

| Name               | Type   | Description                                                                                                                                                           | Required |
| ------------------ | ------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- |
| interactionId      | String | The unique ID represents the task that the user is currently working on. It is generated automatically during the creation of a new task.                                                                                                                           | Yes      |
| data               | Object | Options of the blind transfer request.                                                                                                                                | Yes      |
| -->to         | String | Unique identifier of the agent.                                                                                                                                       | Yes      |
| -->destinationType     | String | The type of consult transfer request to be placed. The destination type can be `agent` or `dialNumber`. | Yes      |

**Returns**
`{Object}` The object with the retrieved data.

**Note:** The `type` parameter value in the response payload depends on the success or failure of the method. If the method is successful, the value is `AgentBlindTransferred`; else, `AgentBlindTransferFailedEvent`.

**Example Response**

```javascript
const blindTransferResponse = {
  data: {
    agentId: "cdf786ef-3285-4b2f-8ef9-3cf8a4c755c2",
    destAgentId: "337c1cca-d79b-44fc-8d8e-20d1b5e4dadf",
    destinationType: "Agent",
    eventType: "RoutingMessage",
    interaction: {
      callAssociatedData: {
        ani: {
          agentEditable: false,
          displayName: "ani",
          name: "ani",
          type: "STRING",
          value: "displayName"
        },
        appUser: {
          agentEditable: false,
          displayName: "appUser",
          name: "appUser",
          type: "STRING",
          value: "qaus1-appuser-1212"
        },
        customerName: {
          agentEditable: false,
          displayName: "customerName",
          name: "customerName",
          type: "STRING",
          value: "displayName"
        },
        dn: {
          agentEditable: false,
          displayName: "dn",
          name: "dn",
          type: "STRING",
          value: "AXVP2lxF0G6K4V3pFKRG"
        },
        ronaTimeout: {
          agentEditable: false,
          displayName: "ronaTimeout",
          name: "ronaTimeout",
          type: "STRING",
          value: "30"
        },
        virtualTeamName: {
          agentEditable: false,
          displayName: "virtualTeamName",
          name: "virtualTeamName",
          type: "STRING",
          value: "QA-e2e-SocialQueue"
        }
      },
      callAssociatedDetails: {
        ani: "***********",
        appUser: "appuser-1212",
        customerName: "displayName",
        dn: "********************",
        ronaTimeout: "30",
        virtualTeamName: "QA-e2e-SocialQueue"
      },
      callFlowParams: {},
      callProcessingDetails: {
        BLIND_TRANSFER_IN_PROGRESS: "true",
        QMgrName: "aqm",
        QueueId: "5134",
        ani: "***********",
        appUser: "qaus1-appuser-1212",
        customerName: "displayName",
        dnis: "********************",
        pauseDuration: "30",
        pauseResumeEnabled: "true",
        ronaTimeout: "30",
        taskToBeSelfServiced: "false",
        tenantId: "82",
        virtualTeamName: "SocialQueue",
        vteamId: "5134"
      },
      contactDirection: {
        type: "INBOUND"
      },
      currentVTeam: "5134",
      interactionId: "1da228dc-66cc-11eb-b852-ed71847d1aec",
      isFcManaged: false,
      isTerminated: false,
      media: {
        Y2lzY29zcGFyazovL3VzL1JPT00vNGQ5NGJmMjAtYjYwZi0xMWVhLTk0YjAtNzdjZDBkYWVjNDA1:
          {
            holdTimestamp: null,
            isHold: false,
            mType: "mainCall",
            mediaMgr: "socialmm",
            mediaResourceId:
              "Y2lzY29zcGFyazovL3VzL1JPT00vNGQ5NGJmMjAtYjYwZi0xMWVhLTk0YjAtNzdjZDBkYWVjNDA1",
            mediaType: "social",
            participants: ["displayName"]
          }
      },
      mediaChannel: "type",
      mediaType: "social",
      orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
      outboundType: null,
      owner: "337c1cca-d79b-44fc-8d8e-20d1b5e4dadf",
      participants: {
        "337c1cca-d79b-44fc-8d8e-20d1b5e4dadf": {
          channelId: "e08a6068-688d-472b-887b-1c5d39c7155f",
          consultState: null,
          consultTimestamp: null,
          dn: "*****",
          hasJoined: false,
          id: "337c1cca-d79b-44fc-8d8e-20d1b5e4dadf",
          isConsulted: false,
          isWrapUp: false,
          joinTimestamp: null,
          lastUpdated: 1612431250963,
          name: "social-agent2",
          pType: "Agent",
          queueId: "5134",
          queueMgrId: "aqm",
          sessionId: "a9aa9867-e62f-4415-9ea4-6babace39d4f",
          siteId: "205",
          teamId: "384",
          teamName: "TeamSales",
          type: "Agent",
          wrapUpTimestamp: null
        },
        "cdf786ef-3285-4b2f-8ef9-3cf8a4c755c2": {
          channelId: "59826e62-08c8-41e6-b51c-4a2b6d81d2f6",
          consultState: null,
          consultTimestamp: null,
          dn: "*****",
          hasJoined: true,
          id: "cdf786ef-3285-4b2f-8ef9-3cf8a4c755c2",
          isConsulted: false,
          isWrapUp: true,
          joinTimestamp: 1612431249042,
          lastUpdated: 1612431251178,
          name: "qaus1-gt-social-agent1 qaus1-gt-social-agent1",
          pType: "Agent",
          queueId: "5134",
          queueMgrId: "aqm",
          sessionId: "600e7ebb-20aa-4c91-a4f0-ebc596249603",
          siteId: "205",
          teamId: "384",
          teamName: "TeamSales",
          type: "Agent",
          wrapUpTimestamp: 1612431251178
        },
        displayName: {
          id: "displayName",
          pType: "Customer",
          type: "Customer"
        }
      },
      previousVTeams: ["AXVP2lxF0G6K4V3pFKRG"],
      state: "new",
      workflowManager: null
    },
    interactionId: "1da228dc-66cc-11eb-b852-ed71847d1aec",
    mediaResourceId:
      "Y2lzY29zcGFyazovL3VzL1JPT00vNGQ5NGJmMjAtYjYwZi0xMWVhLTk0YjAtNzdjZDBkYWVjNDA1",
    orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
    queueMgr: "aqm",
    trackingId: "4a958ace-49a2-49aa-b2e5-8798ede03f13",
    type: "AgentBlindTransferred"
  },
  orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
  trackingId: "notifs_68c519c8-04f5-48b4-a5cf-609a09ccd765",
  type: "RoutingMessage"
};
```
