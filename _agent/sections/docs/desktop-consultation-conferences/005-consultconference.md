---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-consultation-conferences
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Agent Contact Methods
- consultConference()
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

### consultConference()

**Deprecated:** Since May 16, 2025. Use [consultConferenceV2()](https://developer.webex.com/docs/desktop-consultation-conferences#consultconferencev2) instead.

Initiates a conference request with one of the agents from the list of buddyAgents.

**Example**

```javascript
await Desktop.agentContact.consultConference({
    interactionId: "a26d035d-b547-11ea-984b-d3128111ce6b",
    data: {
        agentId: "43bfcdef-5551-45b1-a8f9-a0b33e66e3fe",
        destAgentId: "f795f41f-3782-44fa-97a4-c8b4dc029477",
        mediaType: "chat"
    }
});
```

**Payload type**

```typescript
type ConsultConferencePayload = {
    interactionId: string;data: ConsultPayload | ConsultDN
}

type ConsultDN = {
    destAgentId: string;
    destinationType: string;
    mediaType: string;
    trackingId ?: string | undefined;
}

type ConsultPayload = {
    agentId: string;
    destAgentId: string | undefined;
    mediaType ?: string | undefined;
}
```

The following table lists the payload details:

| Name               | Type   | Description                                                                                           | Required |
| ------------------ | ------ | ----------------------------------------------------------------------------------------------------- | -------- |
| interactionId      | String | Unique identifier for the user interaction.                                                           | Yes      |
| data               | Object | Options of the conference request.                                                                    | Yes      |
| -->agentId         | String | Unique identifier of the agent.                                                                       | For agent consultations |
| -->destAgentId     | String | Unique identifier of the conference request destination agent.                                        | For dial-number consultations; optional for agent consultations |
| -->mediaType       | String | The media channel type such as chat.                                                                  | For dial-number consultations; optional for agent consultations |
| -->destinationType | String | The type of consult conference request to be placed. The destination type can be Agent, Queue, or DN. | For dial-number consultations |
| -->trackingId      | String | Unique identifier based on the conference request type.                                               | No |

**Returns**
`{Object}` The object with the retrieved data.

**Note:** The `type` parameter value in the response payload depends on the success or failure of the method. If the method is successful, the value is`AgentConsultConferenced`; else, `AgentConsultConferenceFailed`.

**Example Response**

```javascript
const consultConferenceResponse = {
  data: {
    agentId: "337c1cca-d79b-44fc-8d8e-20d1b5e4dadf",
    consultMediaResourceId:
      "consult_Y2lzY29zcGFyazovL3VzL1JPT00vNGQ5NGJmMjAtYjYwZi0xMWVhLTk0YjAtNzdjZDBkYWVjNDA1",
    destAgentId: "cdf786ef-3285-4b2f-8ef9-3cf8a4c755c2",
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
          value: "appuser-1212"
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
        QMgrName: "aqm",
        QueueId: "5134",
        ani: "***********",
        appUser: "appuser-1212",
        customerName: "displayName",
        dnis: "********************",
        pauseDuration: "30",
        pauseResumeEnabled: "true",
        ronaTimeout: "30",
        taskToBeSelfServiced: "false",
        tenantId: "82",
        virtualTeamName: "QA-e2e-SocialQueue",
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
            participants: [
              "displayName",
              "337c1cca-d79b-44fc-8d8e-20d1b5e4dadf",
              "cdf786ef-3285-4b2f-8ef9-3cf8a4c755c2"
            ]
          },
        consult_Y2lzY29zcGFyazovL3VzL1JPT00vNGQ5NGJmMjAtYjYwZi0xMWVhLTk0YjAtNzdjZDBkYWVjNDA1:
          {
            holdTimestamp: null,
            isHold: false,
            mType: "consult",
            mediaMgr: "socialmm",
            mediaResourceId:
              "consult_Y2lzY29zcGFyazovL3VzL1JPT00vNGQ5NGJmMjAtYjYwZi0xMWVhLTk0YjAtNzdjZDBkYWVjNDA1",
            mediaType: "social",
            participants: [
              "cdf786ef-3285-4b2f-8ef9-3cf8a4c755c2",
              "337c1cca-d79b-44fc-8d8e-20d1b5e4dadf",
              "cdf786ef-3285-4b2f-8ef9-3cf8a4c755c2"
            ]
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
          consultState: "conferencing",
          consultTimestamp: 1612431260416,
          dn: "*****",
          hasJoined: true,
          id: "337c1cca-d79b-44fc-8d8e-20d1b5e4dadf",
          isConsulted: false,
          isWrapUp: false,
          joinTimestamp: 1612431253790,
          lastUpdated: 1612431253790,
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
          channelId: "841235e4-7052-455b-be64-30f2f3c4a59b",
          consultState: "conferencing",
          consultTimestamp: 1612431260416,
          dn: "*****",
          hasJoined: true,
          id: "cdf786ef-3285-4b2f-8ef9-3cf8a4c755c2",
          isConsulted: true,
          isWrapUp: false,
          joinTimestamp: 1612431258137,
          lastUpdated: 1612431258137,
          name: "social-agent1",
          pType: "Agent",
          queueId: "5134",
          queueMgrId: "aqm",
          sessionId: "600e7ebb-20aa-4c91-a4f0-ebc596249603",
          siteId: "205",
          teamId: "384",
          teamName: "TeamSales",
          type: "Agent",
          wrapUpTimestamp: null
        },
        displayName: {
          id: "displayName",
          pType: "Customer",
          type: "Customer"
        }
      },
      previousVTeams: ["AXVP2lxF0G6K4V3pFKRG"],
      state: "conference",
      workflowManager: null
    },
    interactionId: "1da228dc-66cc-11eb-b852-ed71847d1aec",
    mediaResourceId:
      "Y2lzY29zcGFyazovL3VzL1JPT00vNGQ5NGJmMjAtYjYwZi0xMWVhLTk0YjAtNzdjZDBkYWVjNDA1",
    orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
    queueMgr: "aqm",
    trackingId: "4a958ace-49a2-49aa-b2e5-8798ede03f13",
    type: "AgentConsultConferenced"
  },
  orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
  trackingId: "notifs_68c519c8-04f5-48b4-a5cf-609a09ccd765",
  type: "RoutingMessage"
};
```
