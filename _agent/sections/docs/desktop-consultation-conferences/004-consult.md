---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-consultation-conferences
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Agent Contact Methods
- consult()
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

### consult()

**Deprecated:** Since May 16, 2025. Use [consultV2()](https://developer.webex.com/docs/desktop-consultation-conferences#consultv2) instead.

Initiates a consult request with an agent, a dial number (DN), or a queue.

**Note:** The consult call to queue feature is enabled using the allowConsultToQueue payload. For more information, see [Agent State Information Module](https://developer.webex.com/docs/desktop-agent-state#agent-state-information-module).

**Example**

```javascript
await Desktop.agentContact.consult({
    interactionId: "a26d035d-b547-11ea-984b-d3128111ce6b",
    data: {
        agentId: "43bfcdef-5551-45b1-a8f9-a0b33e66e3fe",
        destAgentId: "f795f41f-3782-44fa-97a4-c8b4dc029477",
        mediaType: "chat"
    },
    url: "consult"
});
```

**Payload type**

```typescript
type RequestPayload = {
    interactionId: string;
    data: ConsultPayload | ConsultDN | ConsultAgent | ConsultQueue;
    url: string;
}

type ConsultPayload = {
    agentId: string;
    destAgentId: string | undefined;
    mediaType ?: string | undefined;
}

type ConsultDN = {
    destAgentId: string;
    destinationType: string;
    mediaType: string;
    trackingId ?: string;
};

type ConsultAgent = {
    agentId: string;
    destAgentId: string;
    destAgentDN ?: string;
    destAgentTeamId ?: string;
    destSiteId ?: string;
    mediaType: string;
    trackingId: string;
};

type ConsultQueue = {
    agentId: string;
    queueId: string;
    trackingId: string;
};
```

The following table lists the payload details:

| Name               | Type   | Description                                                                                | Required |
| ------------------ | ------ | ------------------------------------------------------------------------------------------ | -------- |
| interactionId      | String | Unique identifier for the user interaction.                                                | Yes      |
| data               | Object | Options of the consult request.                                                            | Yes      |
| -->agentId         | String | Unique identifier of the agent.                                                            | For agent and queue consultations      |
| -->destAgentId     | String | Unique identifier of the consult request destination agent.                                | For agent and dial-number consultations      |
| -->mediaType       | String | The media channel type such as chat.                                                       | For agent and dial-number consultations      |
| -->destinationType | String | The type of consult request to be placed. The destination type can be Agent, Queue, or DN. | For dial-number consultations      |
| -->trackingId      | String | Unique identifier based on the consult request type.                                       | For agent and queue consultations; optional for dial-number consultations      |
| -->destAgentDN     | String | The dial number of the destination agent.                                                  | No      |
| -->destAgentTeamId | String | Unique identifier of the team to which the destination agent belongs.                      | No      |
| -->destSiteId      | String | Unique identifier of the destination site.                                                 | No      |
| -->queueId         | String | Unique identifier of the queue.                                                            | For queue consultations      |
| url                | String | The URL of the consult. Example, consult, ctq.                                             | Yes      |

**Returns**
`{Object}` The object with the retrieved data.

**Note:** The `type` parameter value in the response payload depends on the success or failure of the method. If the method is successful, the value is `AgentConsultCreated`; else, `AgentCtqFailed` or `AgentConsultFailed`.

**Example Response**

```javascript
const consultResponse = {
  data: {
    agentId: "7d12d9ea-e8e0-41ee-81bf-c11a685b64ed",
    consultMediaResourceId:
      "consult_Y2lzY29zcGFyazovL3VzL1JPT00vNjJkYjBmMzAtNDBhZi0xMWViLWE3ZGItYjkyYTZkMmI5NTI1",
    destAgentId: "aad323de-32d8-48c9-af6b-b68dfbabfe20",
    destinationType: "Agent",
    eventType: "RoutingMessage",
    interaction: {
      callAssociatedData: {
        ani: {
          value: "janedoe@gmail.com"
        },
        category: {
          value: "Sales"
        },
        customerName: {
          value: "Jane Doe"
        },
        dn: {
          value: "Desktop"
        },
        entryPointId: {
          value: "AXCqFyz1G2pKap9PI-mW"
        },
        guestId: {
          value:
            "Y2lzY29zcGFyazovL3VzL1BFT1BMRS81NzNiODg1Mi1kZjM3LTRlODEtOGMxMi1mZjkyMTE3MmQ1NzY"
        },
        mediaChannel: {
          value: "web"
        },
        reason: {
          value: "test"
        },
        reasonCode: {
          value: "Sales"
        },
        ronaTimeout: {
          value: "30"
        },
        roomTitle: {
          value: "Help Jane Doe with Sales"
        },
        taskToBeSelfServiced: {
          value: "false"
        },
        templateId: {
          value: "b57990c0-5ec6-11ea-96ee-5df5aef56329"
        },
        templateName: {
          value: "Desktop"
        },
        virtualTeamName: {
          agentEditable: false,
          displayName: "virtualTeamName",
          name: "virtualTeamName",
          type: "STRING",
          value: "Chat_Queue"
        }
      },
      callAssociatedDetails: {
        ani: "janedoe@gmail.com",
        category: "Sales",
        customerName: "Jane Doe",
        dn: "Desktop",
        entryPointId: "AXCqFyz1G2pKap9PI-mW",
        guestId:
          "Y2lzY29zcGFyazovL3VzL1BFT1BMRS81NzNiODg1Mi1kZjM3LTRlODEtOGMxMi1mZjkyMTE3MmQ1NzY",
        mediaChannel: "web",
        reason: "test",
        reasonCode: "Sales",
        ronaTimeout: "30",
        roomTitle: "Help Jane Doe with Sales",
        taskToBeSelfServiced: "false",
        templateId: "b57990c0-5ec6-11ea-96ee-5df5aef56329",
        templateName: "Desktop",
        virtualTeamName: "Chat_Queue"
      },
      callFlowParams: {
        Automation: {
          description: "(vteam, A valid VTeam.)",
          name: "Automation",
          qualifier: "vteam",
          value: "3270",
          valueDataType: "string"
        },
        Debit: {
          description: "(vteam, A valid VTeam.)",
          name: "Debit",
          qualifier: "vteam",
          value: "3270",
          valueDataType: "string"
        },
        Sales: {
          description: "(vteam, A valid VTeam.)",
          name: "Sales",
          qualifier: "vteam",
          value: "3270",
          valueDataType: "string"
        }
      },
      callProcessingDetails: {
        QMgrName: "aqm",
        QueueId: "3270",
        ani: "janedoe@gmail.com",
        category: "Sales",
        customerName: "Jane Doe",
        dnis: "Desktop",
        entryPointId: "AXCqFyz1G2pKap9PI-mW",
        guestId:
          "Y2lzY29zcGFyazovL3VzL1BFT1BMRS81NzNiODg1Mi1kZjM3LTRlODEtOGMxMi1mZjkyMTE3MmQ1NzY",
        mediaChannel: "web",
        pauseDuration: "10",
        pauseResumeEnabled: "true",
        reason: "test",
        reasonCode: "Sales",
        ronaTimeout: "30",
        roomTitle: "Help Jane Doe with Sales",
        taskToBeSelfServiced: "false",
        templateId: "b57990c0-5ec6-11ea-96ee-5df5aef56329",
        templateName: "Desktop",
        tenantId: "133",
        virtualTeamName: "Chat_Queue",
        vteamId: "AXCqFyz1G2pKap9PI-mW"
      },
      contactDirection: {
        type: "INBOUND"
      },
      currentVTeam: "3270",
      interactionId: "5622d599-40af-11eb-8606-657fd6cc0548",
      isFcManaged: false,
      isTerminated: false,
      media: {
        Y2lzY29zcGFyazovL3VzL1JPT00vNjJkYjBmMzAtNDBhZi0xMWViLWE3ZGItYjkyYTZkMmI5NTI1:
          {
            holdTimestamp: null,
            isHold: false,
            mType: "mainCall",
            mediaMgr: "cmm",
            mediaResourceId:
              "Y2lzY29zcGFyazovL3VzL1JPT00vNjJkYjBmMzAtNDBhZi0xMWViLWE3ZGItYjkyYTZkMmI5NTI1",
            mediaType: "chat",
            participants: [
              "janedoe@gmail.com",
              "7d12d9ea-e8e0-41ee-81bf-c11a685b64ed"
            ]
          },
        consult_Y2lzY29zcGFyazovL3VzL1JPT00vNjJkYjBmMzAtNDBhZi0xMWViLWE3ZGItYjkyYTZkMmI5NTI1:
          {
            holdTimestamp: null,
            isHold: false,
            mType: "consult",
            mediaMgr: "cmm",
            mediaResourceId:
              "consult_Y2lzY29zcGFyazovL3VzL1JPT00vNjJkYjBmMzAtNDBhZi0xMWViLWE3ZGItYjkyYTZkMmI5NTI1",
            mediaType: "chat",
            participants: [
              "aad323de-32d8-48c9-af6b-b68dfbabfe20",
              "7d12d9ea-e8e0-41ee-81bf-c11a685b64ed"
            ]
          }
      },
      mediaChannel: "web",
      mediaType: "chat",
      orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
      outboundType: null,
      owner: "7d12d9ea-e8e0-41ee-81bf-c11a685b64ed",
      participants: {
        "7d12d9ea-e8e0-41ee-81bf-c11a685b64ed": {
          channelId: "7272c119-821f-485a-b352-29be1f3f0fff",
          consultState: "consultInitiated",
          consultTimestamp: 1608240860457,
          dn: "9997770110",
          hasJoined: true,
          id: "7d12d9ea-e8e0-41ee-81bf-c11a685b64ed",
          isConsulted: false,
          isWrapUp: false,
          joinTimestamp: 1608240840633,
          lastUpdated: 1608240840633,
          name: "uuip-agent4 uuip-agent4",
          pType: "Agent",
          queueId: "3270",
          queueMgrId: "aqm",
          sessionId: "b8c096ab-f9a0-49be-9efd-f8c78e1a7061",
          siteId: "473",
          teamId: "962",
          teamName: "Team X",
          type: "Agent",
          wrapUpTimestamp: null
        },
        "aad323de-32d8-48c9-af6b-b68dfbabfe20": {
          channelId: "b1da7e42-2aeb-492b-ad06-115ba8dfa506",
          consultState: null,
          consultTimestamp: null,
          dn: "9997770109",
          hasJoined: false,
          id: "aad323de-32d8-48c9-af6b-b68dfbabfe20",
          isConsulted: true,
          isWrapUp: false,
          joinTimestamp: null,
          lastUpdated: 1608240860436,
          name: "uuip-agent2 uuip-agent2",
          pType: "Agent",
          queueId: "3270",
          queueMgrId: "aqm",
          sessionId: "3443f9d7-68de-42a0-a590-176a37a3565a",
          siteId: "473",
          teamId: "962",
          teamName: "Team X",
          type: "Agent",
          wrapUpTimestamp: null
        },
        "janedoe@gmail.com": {
          id: "janedoe@gmail.com",
          pType: "Customer",
          type: "Customer"
        }
      },
      previousVTeams: [],
      state: "consult"
    },
    interactionId: "5622d599-40af-11eb-8606-657fd6cc0548",
    mediaResourceId:
      "Y2lzY29zcGFyazovL3VzL1JPT00vNjJkYjBmMzAtNDBhZi0xMWViLWE3ZGItYjkyYTZkMmI5NTI1",
    orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
    queueMgr: "aqm",
    trackingId: "9f682870-40af-11eb-bc9c-df3ff755538c",
    type: "AgentConsultCreated"
  },
  orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
  trackingId: "notifs_6dc77353-e810-4751-82ac-dab03e3951c2",
  type: "RoutingMessage"
};
```
