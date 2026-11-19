---
type: Guide
title: Consultation and Conferences
display_title: Consultation and Conferences
canonical_url: https://developer.webex.com/docs/desktop-consultation-conferences
content_type: documentation
product_group:
- webex-contact-center
categories:
- webex-contact-center
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/desktop-consultation-conferences)

Use the Desktop SDK to consult agents and queues and manage conference participants.

## Before You Begin

Install and initialize the SDK as described in [Get Started with the Desktop SDK](https://developer.webex.com/docs/desktop-sdk-getting-started). Your widget must run inside Webex Contact Center Desktop.

## Agent Contact Methods

These methods belong to `Desktop.agentContact`. Use the V2 method where the older method is marked for deprecation.

### consultAccept()

Accepts a consult task.

**Example**

```javascript
await Desktop.agentContact.consultAccept({
    interactionId: "c837e6f7-699a-4736-bb82-03a6d58bb7f3"
});
```

The following table lists the payload details:

| Name          | Type   | Description                                 | Required |
| ------------- | ------ | ------------------------------------------- | -------- |
| interactionId | String | Unique identifier for the user interaction. | Yes      |

**Returns**

`{Object}` The value that corresponds to the task.

**Note:** The `type` parameter value in the response payload depends on the success or failure of the method. If the method is successful, the value is `AgentConsulting`; else, `AgentContactAssignFailed`.

**Example Response**

```javascript
const consultAcceptResponse = {
  data: {
    agentId: "9b036d89-930c-4187-a5bd-5dbb1439fe41",
    consultMediaResourceId: "c1b507d0-9aac-4500-a9f8-50f30eba4310",
    destAgentId: "ff7dbe19-fa3f-4c63-8a1c-04dcffef8e4f",
    destinationType: "Agent",
    eventType: "RoutingMessage",
    interaction: {
      callAssociatedData: {
        "": {
          agentEditable: false,
          displayName: "",
          name: "",
          type: "STRING",
          value: ""
        },
        IvrPath: {
          agentEditable: false,
          displayName: "IvrPath",
          name: "IvrPath",
          type: "STRING",
          value: " EOI"
        },
        ani: {
          agentEditable: false,
          displayName: "ani",
          name: "ani",
          type: "STRING",
          value: "**********"
        },
        dn: {
          agentEditable: false,
          displayName: "dn",
          name: "dn",
          type: "STRING",
          value: "**********"
        },
        nextVteamId: {
          agentEditable: false,
          displayName: "nextVteamId",
          name: "nextVteamId",
          type: "STRING",
          value: "Queue"
        },
        pathId: {
          agentEditable: false,
          displayName: "pathId",
          name: "pathId",
          type: "STRING",
          value: " StartCall PlayDone"
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
          value: "Queue-1"
        }
      },
      callAssociatedDetails: {
        "": "",
        IvrPath: " EOI",
        ani: "************",
        dn: "************",
        nextVteamId: "Queue",
        pathId: " StartCall PlayDone",
        ronaTimeout: "30",
        virtualTeamName: "Queue-1"
      },
      callFlowParams: {
        Queue: {
          description: "(vteam, A valid VTeam.)",
          name: "Queue",
          qualifier: "vteam",
          value: "1336",
          valueDataType: "string"
        },
        WelcomePrompt: {
          description: "(mediaFile, A valid media file.)",
          name: "WelcomePrompt",
          qualifier: "mediaFile",
          value: "GAwelcome.wav",
          valueDataType: "string"
        }
      },
      callProcessingDetails: {
        QMgrName: "aqm",
        QueueId: "1336",
        ani: "************",
        dnis: "************",
        isPaused: "false",
        jscriptId: "AW7HP3QNB44q0sL-cTVz",
        pauseDuration: "30",
        pauseResumeEnabled: "true",
        recordInProgress: "true",
        ronaTimeout: "30",
        taskToBeSelfServiced: "false",
        tenantId: "82",
        virtualTeamName: "Queue-1",
        vteamId: "1336"
      },
      contactDirection: {
        type: "INBOUND"
      },
      currentVTeam: "1336",
      interactionId: "1277da79-dc49-439c-ab72-f00453a1ff71",
      isFcManaged: false,
      isTerminated: false,
      media: {
        "1277da79-dc49-439c-ab72-f00453a1ff71": {
          holdTimestamp: 1612429578817,
          isHold: true,
          mType: "mainCall",
          mediaMgr: "vmm",
          mediaResourceId: "1277da79-dc49-439c-ab72-f00453a1ff71",
          mediaType: "telephony",
          participants: ["**********", "9b036d89-930c-4187-a5bd-5dbb1439fe41"]
        },
        "c1b507d0-9aac-4500-a9f8-50f30eba4310": {
          holdTimestamp: null,
          isHold: false,
          mType: "consult",
          mediaMgr: "vmm",
          mediaResourceId: "c1b507d0-9aac-4500-a9f8-50f30eba4310",
          mediaType: "telephony",
          participants: [
            "ff7dbe19-fa3f-4c63-8a1c-04dcffef8e4f",
            "9b036d89-930c-4187-a5bd-5dbb1439fe41",
            "ff7dbe19-fa3f-4c63-8a1c-04dcffef8e4f"
          ]
        }
      },
      mediaChannel: "broadcloud",
      mediaType: "telephony",
      orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
      outboundType: null,
      owner: "9b036d89-930c-4187-a5bd-5dbb1439fe41",
      participants: {
        "**********": {
          id: "**********",
          pType: "Customer",
          type: "Customer"
        },
        "9b036d89-930c-4187-a5bd-5dbb1439fe41": {
          channelId: "3de6706f-95b7-485a-9304-30928f7ee52e",
          consultState: "consulting",
          consultTimestamp: 1612429579220,
          dn: "**********",
          hasJoined: true,
          id: "9b036d89-930c-4187-a5bd-5dbb1439fe41",
          isConsulted: true,
          isWrapUp: false,
          joinTimestamp: 1612429549032,
          lastUpdated: 1612429549032,
          name: "user1",
          pType: "Agent",
          queueId: "1336",
          queueMgrId: "aqm",
          sessionId: "90896c91-0f77-4bc6-aec3-488a34ca88d3",
          siteId: "205",
          teamId: "598",
          teamName: "integ-test-team",
          type: "Agent",
          wrapUpTimestamp: null
        },
        "ff7dbe19-fa3f-4c63-8a1c-04dcffef8e4f": {
          channelId: "fb704337-71c3-4802-a03b-84a2d18eeaa0",
          consultState: "consulting",
          consultTimestamp: 1612429579220,
          dn: "**********",
          hasJoined: true,
          id: "ff7dbe19-fa3f-4c63-8a1c-04dcffef8e4f",
          isConsulted: true,
          isWrapUp: false,
          joinTimestamp: 1612429579200,
          lastUpdated: 1612429579200,
          name: "user2",
          pType: "Agent",
          queueId: "1336",
          queueMgrId: "aqm",
          sessionId: "57323f8b-9460-45fa-aaf6-4ca51c327af8",
          siteId: "205",
          teamId: "598",
          teamName: "integ-test-team",
          type: "Agent",
          wrapUpTimestamp: null
        }
      },
      previousVTeams: ["AW6h1AVRrZSGni185x28"],
      state: "consulting",
      workflowManager: null
    },
    interactionId: "1277da79-dc49-439c-ab72-f00453a1ff71",
    orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
    queueMgr: "aqm",
    trackingId: "e7c032be-b18e-4b63-8ab2-6baf50b137b1",
    type: "AgentConsulting"
  },
  orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
  trackingId: "notifs_3464be63-83e7-4b2d-94d5-a63fddc108d5",
  type: "RoutingMessage"
};
```

### buddyAgents()

**Deprecated:** Since May 16, 2025. Use [buddyAgentsV2()](https://developer.webex.com/docs/desktop-consultation-conferences#buddyagentsv2) instead.

Fetches the list of agents available for consult call and conference call.

**Example**

```
await Desktop.agentContact.buddyAgents({
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

### consultEnd()

**Deprecated:** Since May 16, 2025. Use [consultEndV2()](https://developer.webex.com/docs/desktop-consultation-conferences#consultendv2) instead.


Ends a consult request.
**Note:** The end consult call feature is enabled using the isEndConsultEnabled payload. For more information, see [Agent State Information Module](https://developer.webex.com/docs/desktop-agent-state#agent-state-information-module).

**Example**

```javascript
await Desktop.agentContact.consultEnd({
    interactionId: "a26d035d-b547-11ea-984b-d3128111ce6b",
    isConsult: true
});
```

**Payload type**

```typescript
type RequestPayload = {
    interactionId: string;isConsult: boolean
};
```

The following table lists the payload details:

| Name          | Type    | Description                                                                                                                                   | Required |
| ------------- | ------- | --------------------------------------------------------------------------------------------------------------------------------------------- | -------- |
| interactionId | String  | Unique identifier for the user interaction.                                                                                                   | Yes      |
| isConsult     | Boolean | Determines whether the task request is consult or not.<br><br>- True—The task request is consult.<br>- False—The task request is not consult. | Yes      |

**Returns**
`{Object}` The object with the retrieved data.

**Note:** The `type` parameter value in the response payload depends on the success or failure of the method. If the method is successful, and `isConsult` is _true_, the value is `AgentConsultEnded`; else, `AgentConsultConferenceEnded`. If the method is unsuccessful, the value is `AgentConsultEndFailed`.

**Example Response**

```javascript
const consultEndResponse = {
  data: {
    agentId: "7c867aa9-ec768-341a-b767-e5hd6ae7g701",
    consultMediaResourceId: "f23b5b8a-4b02-451e-b9f5-8517b5bef97c",
    destAgentId: "9fca6158-a8bd-43e6-aeba-e5055aea08c5",
    destinationType: "Agent",
    eventType: "RoutingMessage",
    interaction: {
      callAssociatedData: {
        dn: {
          agentEditable: false,
          displayName: "dn",
          name: "dn",
          type: "STRING",
          value: "8895579172"
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
          value: "Outdial Queue-1"
        }
      },
      callAssociatedDetails: {
        dn: "8895579172",
        ronaTimeout: "30",
        virtualTeamName: "Outdial Queue-1"
      },
      callFlowParams: {
        OutdialQueue: {
          description: "(vteam, The Outdial Queue.)",
          name: "OutdialQueue",
          qualifier: "vteam",
          value: "3264",
          valueDataType: "string"
        }
      },
      callProcessingDetails: {
        QMgrName: "aqm",
        QueueId: "3264",
        dnis: "8895579172",
        isPaused: "false",
        outdialTransferToQueueEnabled: "false",
        pauseDuration: "10",
        pauseResumeEnabled: "true",
        recordInProgress: "true",
        ronaTimeout: "30",
        taskToBeSelfServiced: "false",
        tenantId: "133",
        virtualTeamName: "Outdial Queue-1",
        vteamId: "AXCLfZZU9S1oTdqE1OFZ"
      },
      contactDirection: {
        type: "OUTBOUND"
      },
      currentVTeam: "3264",
      interactionId: "1dd08726-bca5-4ce8-9b51-b20dca8ab154",
      isFcManaged: false,
      isTerminated: false,
      media: {
        "1dd08726-bca5-4ce8-9b51-b20dca8ab154": {
          holdTimestamp: 1612356600241,
          isHold: true,
          mType: "mainCall",
          mediaMgr: "vmm",
          mediaResourceId: "1dd08726-bca5-4ce8-9b51-b20dca8ab154",
          mediaType: "telephony",
          participants: [""]
        }
      },
      mediaChannel: "dialer",
      mediaType: "telephony",
      orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
      outboundType: "OUTDIAL",
      owner: "7c867aa9-ec768-341a-b767-e5hd6ae7g701",
      participants: {
        "": {
          id: "",
          pType: "Customer",
          type: "Customer"
        },
        "7c867aa9-ec768-341a-b767-e5hd6ae7g701": {
          channelId: "0717a2ce-76cd-4ba4-9053-71f2c78168b8",
          consultState: null,
          consultTimestamp: null,
          dn: "8895579172",
          hasJoined: true,
          id: "7c867aa9-ec768-341a-b767-e5hd6ae7g701",
          isConsulted: false,
          isWrapUp: false,
          joinTimestamp: 1612354635705,
          lastUpdated: 1612354635705,
          name: "John Doe",
          pType: "Agent",
          queueId: "3264",
          queueMgrId: "aqm",
          sessionId: "3d017488-527a-4e89-9313-5d4eb353c789",
          siteId: "472",
          teamId: "960",
          teamName: "Email_Team",
          type: "Agent",
          wrapUpTimestamp: null
        }
      },
      previousVTeams: [],
      state: "connected",
      workflowManager: null
    },
    interactionId: "1dd08726-bca5-4ce8-9b51-b20dca8ab154",
    orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
    queueMgr: "aqm",
    trackingId: "f7c7ecd2-ef27-4273-bc11-1543bddc8810",
    type: "AgentConsultEnded"
  },
  orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
  trackingId: "notifs_860d1e16-88b8-4d6c-8bac-18075d72a7e8",
  type: "RoutingMessage"
};
```

### decline()

Declines a consult request.

**Example**

```javascript
await Desktop.agentContact.decline({
    interactionId: "c837e6f7-699a-4736-bb82-03a6d58bb7f3",
    data: {
        mediaResourceId: "c837e6f7-699a-4736-bb82-03a6d58bb7f3"
    },
    isConsult: true,
});
```

**Payload type**

```typescript
type RequestPayload = {
    interactionId: string;
    data: declinePayload;
    isConsult: boolean
}

type declinePayload = {
    mediaResourceId: string;
};
```

The following table lists the payload details:

| Name          | Type    | Description                                                                                                                                   | Required |
| ------------- | ------- | --------------------------------------------------------------------------------------------------------------------------------------------- | -------- |
| interactionId | String  | Unique identifier for the user interaction.                                                                                                   | Yes      |
| data | Object | Options of the decline request. | Yes |
| -->mediaResourceId | String | Identifier of the media resource being declined. | Yes |
| isConsult     | Boolean | Determines whether the task request is consult or not.<br><br>- True—The task request is consult.<br>- False—The task request is not consult. | Yes      |

**Returns**
`{Object}` The object with the retrieved data.

**Note:** The `type` parameter value in the response payload depends on the success or failure of the method. If the method is successful, and `isConsult` is _true_, the value is `AgentConsultFailed`; else, `AgentOfferContactRona`.

**Example Response**

```javascript
const declineResponse = {
  data: {
    agentId: "7c867aa9-ec768-341a-b767-e5hd6ae7g701",
    destAgentId: "f795f41f-3782-44fa-97a4-c8b4dc029477",
    destinationType: "Agent",
    eventType: "RoutingMessage",
    interaction: {
      callAssociatedData: {},
      callAssociatedDetails: {},
      callFlowParams: {},
      callProcessingDetails: {},
      contactDirection: {
        type: "INBOUND"
      },
      currentVTeam: "",
      interactionId: "9ad96648-415b-11eb-881c-ed6dd0d45a04",
      isFcManaged: false,
      isTerminated: false,
      media: {},
      mediaChannel: "none",
      mediaType: "none",
      orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
      outboundType: null,
      owner: null,
      participants: {},
      previousVTeams: [],
      state: "none",
      workflowManager: null
    },
    interactionId: "a26d035d-b547-11ea-984b-d3128111ce6b",
    orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
    queueMgr: "aqm",
    reason: "Test",
    reasonCode: 500,
    trackingId: "2037cb70-653d-11eb-8a11-a3c35f103d4b",
    type: "AgentConsultFailed"
  },
  orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
  trackingId: "notifs_a241b1c4-3d42-4ad0-8738-71b1e7611550",
  type: "RoutingMessage"
};
```

### cancelCtq()

Cancels a consult to queue request.

**Example**

```javascript
await Desktop.agentContact.cancelCtq({
    interactionId: "a26d035d-b547-11ea-984b-d3128111ce6b",
    data: {
        agentId: "f795f41f-3782-44fa-97a4-c8b4dc029477",
        queueId: "3268"
    }
});

```

**Payload type**

```typescript
type CancelCtqPayload = {
    interactionId: string;
    data: { agentId: string; queueId: string };
};
```

The following table lists the payload details:

| Name          | Type   | Description                                 | Required |
| ------------- | ------ | ------------------------------------------- | -------- |
| interactionId | String | Unique identifier for the user interaction. | Yes      |
| data          | Object | Options of the consult to queue request.    | Yes      |
| -->agentId    | String | Unique identifier of the agent.             | Yes      |
| -->queueId    | String | Unique identifier of the queue.             | Yes      |

**Returns**
`{Object}` The object with the retrieved data.

**Note:** The `type` parameter value in the response payload depends on the success or failure of the method. If the method is successful, the value is `AgentCtqCancelled`; else, `AgentCtqCancelFailed`.

**Example Response**

```javascript
const cancelCtqResponse = {
  data: {
    agentId: "a96ffe92-f5c8-4715-9427-fa32a7e57ccc",
    eventType: "RoutingMessage",
    interaction: {
      callAssociatedData: {},
      callAssociatedDetails: {},
      callFlowParams: {},
      callProcessingDetails: {},
      contactDirection: {
        type: "INBOUND"
      },
      currentVTeam: "",
      interactionId: "9ad96648-415b-11eb-881c-ed6dd0d45a04",
      isFcManaged: false,
      isTerminated: false,
      media: {},
      mediaChannel: "none",
      mediaType: "none",
      orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
      outboundType: null,
      owner: null,
      participants: {},
      previousVTeams: [],
      state: "none"
    },
    interactionId: "c8e35eec-a977-409b-922d-7d2825c63cf2",
    orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
    queueId: "7352",
    queueMgr: "aqm",
    trackingId: "ee2bc7e0-50c8-11eb-a1f8-5d0ad357b8a5",
    type: "AgentCtqCancelled"
  },
  orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
  trackingId: "notifs_908141bb-3f1f-43fe-b7e2-5a132c97745f",
  type: "RoutingMessage"
};
```

### consultV2()

Initiates a consult request with an agent, a dial number (DN), a entrypoint or a queue.

**Note:** The consult call to queue feature is enabled using the allowConsultToQueue payload. For more information, see [Agent State Information Module](https://developer.webex.com/docs/desktop-agent-state#agent-state-information-module).

**Example**

```javascript
await Desktop.agentContact.consultV2({
    interactionId: "a26d035d-b547-11ea-984b-d3128111ce6b",
    data: {
        to: "43bfcdef-5551-45b1-a8f9-a0b33e66e3fe",
        destinationType: "agent",
        holdParticipants: true
    }
});
```

**Payload type**

```typescript
type consultDataV2 = {
  to: string | undefined;
  destinationType: string;
  holdParticipants?: boolean;
};
```

The following table lists the payload details:

| Name               | Type   | Description                                                                                | Required |
| ------------------ | ------ | ------------------------------------------------------------------------------------------ | -------- |
| interactionId      | String | Unique identifier for the user interaction.                                                | Yes      |
| data               | Object | Options of the consult request.                                                            | Yes      |
| -->to         | String | Unique identifier a agentId or a queueId, or a dialNumber or a entryPointId.                                                            | Yes      |
| -->destinationType | String | The type of consult request to be placed. The destination type can be agent, queue, or dialNumber, or entryPoint. | Yes      |
| -->holdParticipants | Boolean | Determines whether to hold the participants during consultation. | No |

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

### consultEndV2()

Ends a consult request.
**Note:** The end consult call feature is enabled using the `isEndConsultEnabled` payload. For more information, see [Agent State Information Module](https://developer.webex.com/docs/desktop-agent-state#agent-state-information-module).

**Example**

```javascript
await Desktop.agentContact.consultEndV2({
    interactionId: "a26d035d-b547-11ea-984b-d3128111ce6b",
    isConsult: true
});
```

**Payload type**

```typescript
type RequestPayload = {
    interactionId: string;isConsult: boolean;isSecondaryEpDnAgent?: boolean;queueId?: string;
};
```

The following table lists the payload details:

| Name          | Type    | Description                                                                                                                                   | Required |
| ------------- | ------- | --------------------------------------------------------------------------------------------------------------------------------------------- | -------- |
| interactionId | String  | Unique identifier for the user interaction.                                                                                                   | Yes      |
| isConsult     | Boolean | Determines whether the task request is consult or not.<br><br>- True—The task request is consult.<br>- False—The task request is not consult. | Yes      |
| isSecondaryEpDnAgent | Boolean | Indicates whether the requesting agent is the secondary agent for an entry point or dial-number consultation. Supply when applicable. | No |
| queueId | String | Identifier of the queue for a consultation made to a queue. Supply for queue consultations. | No |

**Returns**
`{Object}` The object with the retrieved data.

**Note:** The `type` parameter value in the response payload depends on the success or failure of the method. If the method is successful, and `isConsult` is _true_, the value is `AgentConsultEnded`; else, `AgentConsultConferenceEnded`. If the method is unsuccessful, the value is `AgentConsultEndFailed`.

**Example Response**

```javascript
const consultEndResponse = {
  data: {
    agentId: "7c867aa9-ec768-341a-b767-e5hd6ae7g701",
    consultMediaResourceId: "f23b5b8a-4b02-451e-b9f5-8517b5bef97c",
    destAgentId: "9fca6158-a8bd-43e6-aeba-e5055aea08c5",
    destinationType: "Agent",
    eventType: "RoutingMessage",
    interaction: {
      callAssociatedData: {
        dn: {
          agentEditable: false,
          displayName: "dn",
          name: "dn",
          type: "STRING",
          value: "8895579172"
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
          value: "Outdial Queue-1"
        }
      },
      callAssociatedDetails: {
        dn: "8895579172",
        ronaTimeout: "30",
        virtualTeamName: "Outdial Queue-1"
      },
      callFlowParams: {
        OutdialQueue: {
          description: "(vteam, The Outdial Queue.)",
          name: "OutdialQueue",
          qualifier: "vteam",
          value: "3264",
          valueDataType: "string"
        }
      },
      callProcessingDetails: {
        QMgrName: "aqm",
        QueueId: "3264",
        dnis: "8895579172",
        isPaused: "false",
        outdialTransferToQueueEnabled: "false",
        pauseDuration: "10",
        pauseResumeEnabled: "true",
        recordInProgress: "true",
        ronaTimeout: "30",
        taskToBeSelfServiced: "false",
        tenantId: "133",
        virtualTeamName: "Outdial Queue-1",
        vteamId: "AXCLfZZU9S1oTdqE1OFZ"
      },
      contactDirection: {
        type: "OUTBOUND"
      },
      currentVTeam: "3264",
      interactionId: "1dd08726-bca5-4ce8-9b51-b20dca8ab154",
      isFcManaged: false,
      isTerminated: false,
      media: {
        "1dd08726-bca5-4ce8-9b51-b20dca8ab154": {
          holdTimestamp: 1612356600241,
          isHold: true,
          mType: "mainCall",
          mediaMgr: "vmm",
          mediaResourceId: "1dd08726-bca5-4ce8-9b51-b20dca8ab154",
          mediaType: "telephony",
          participants: [""]
        }
      },
      mediaChannel: "dialer",
      mediaType: "telephony",
      orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
      outboundType: "OUTDIAL",
      owner: "7c867aa9-ec768-341a-b767-e5hd6ae7g701",
      participants: {
        "": {
          id: "",
          pType: "Customer",
          type: "Customer"
        },
        "7c867aa9-ec768-341a-b767-e5hd6ae7g701": {
          channelId: "0717a2ce-76cd-4ba4-9053-71f2c78168b8",
          consultState: null,
          consultTimestamp: null,
          dn: "8895579172",
          hasJoined: true,
          id: "7c867aa9-ec768-341a-b767-e5hd6ae7g701",
          isConsulted: false,
          isWrapUp: false,
          joinTimestamp: 1612354635705,
          lastUpdated: 1612354635705,
          name: "John Doe",
          pType: "Agent",
          queueId: "3264",
          queueMgrId: "aqm",
          sessionId: "3d017488-527a-4e89-9313-5d4eb353c789",
          siteId: "472",
          teamId: "960",
          teamName: "Email_Team",
          type: "Agent",
          wrapUpTimestamp: null
        }
      },
      previousVTeams: [],
      state: "connected",
      workflowManager: null
    },
    interactionId: "1dd08726-bca5-4ce8-9b51-b20dca8ab154",
    orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
    queueMgr: "aqm",
    trackingId: "f7c7ecd2-ef27-4273-bc11-1543bddc8810",
    type: "AgentConsultEnded"
  },
  orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
  trackingId: "notifs_860d1e16-88b8-4d6c-8bac-18075d72a7e8",
  type: "RoutingMessage"
};
```

### consultConferenceV2()

Initiates a conference request with consulting agent.

**Example**

```javascript
await Desktop.agentContact.consultConferenceV2({
    interactionId: "a26d035d-b547-11ea-984b-d3128111ce6b",
    data: {
      to: "b66d035d-b547-11ea-984b-d3128111cedb",
      destinationType: "agent",
    }
});
```

**Payload type**

```typescript
type consultConferenceDataV2 = {
  to: string | undefined;
  destinationType: string;
};
```

The following table lists the payload details:

| Name               | Type   | Description                                                                                           | Required |
| ------------------ | ------ | ----------------------------------------------------------------------------------------------------- | -------- |
| interactionId      | String | Unique identifier for the user interaction.                                                           | Yes      |
| data               | Object | Options of the conference request.                                                                    | Yes      |
| -->to         | String | Destination identifier or value for the selected destination type (agent ID, queue ID, dial number, or entry point ID).                                                                       | Yes      |
| -->destinationType | String | The type of consult conference request to be placed. The V2 destination types are `agent`, `queue`, `dialNumber`, and `entryPoint`. | Yes      |

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

### exitConference()

exits a conference request.
**Note:** The end consult call feature is enabled using the `isEndConsultEnabled` payload. For more information, see [Agent State Information Module](https://developer.webex.com/docs/desktop-agent-state#agent-state-information-module).

**Example**

```javascript
await Desktop.agentContact.exitConference({
    interactionId: "a26d035d-b547-11ea-984b-d3128111ce6b"
});

```

**Payload type**

```typescript
type ExitConferencePayload = {
    interactionId: string;
};
```

The following table lists the payload details:

| Name          | Type    | Description                                                                                                                                   | Required |
| ------------- | ------- | --------------------------------------------------------------------------------------------------------------------------------------------- | -------- |
| interactionId | String  | Unique identifier for the user interaction.                                                                                                   | Yes      |

**Returns**
`{Object}` The object with the retrieved data.

**Note:** The successful response example has `type: "AgentConsultConferenceEnded"`. Subscribe to `eAgentConsultConferenceEndFailed` to handle a failed conference-end request; see [Contact Events and Subscriptions](https://developer.webex.com/docs/desktop-contact-events#eagentconsultconferenceendfailed).

**Example Response**

```javascript
const exitConferenceResponse = {
  "data": {
    "agentId": "366f2a3a-dd91-482f-b57e-1abf93dda1f7",
    "consultMediaResourceId": "0b09cfec-feea-4ccf-a78a-b7b06d485be2",
    "destAgentId": "3b05f0e9-48e5-40c9-8923-c50e9b0b22a7",
    "destinationType": "Agent",
    "eventTime": 1728979843658,
    "eventType": "RoutingMessage",
    "force": false,
    "interaction": {
      "callAssociatedData": {
        "CallDate": {
          "agentEditable": true,
          "agentViewable": true,
          "displayName": "CallDate",
          "global": false,
          "isSecure": false,
          "name": "CallDate",
          "reportable": false,
          "secureKeyId": "",
          "secureKeyVersion": 0,
          "type": "DATETIME",
          "value": "2024-10-15T08:09:54.214Z[UTC]"
        },
        "Customer_Name": {
          "agentEditable": true,
          "agentViewable": true,
          "displayName": "Customer_Name",
          "global": false,
          "isSecure": false,
          "name": "Customer_Name",
          "reportable": false,
          "secureKeyId": "",
          "secureKeyVersion": 0,
          "type": "STRING",
          "value": "ModiJi"
        },
        "Global_FeedbackSurveyOptIn": {
          "agentEditable": true,
          "agentViewable": true,
          "displayName": "Post Call Survey Opt-in",
          "global": true,
          "isSecure": false,
          "name": "Global_FeedbackSurveyOptIn",
          "reportable": true,
          "secureKeyId": "",
          "secureKeyVersion": 0,
          "type": "STRING",
          "value": "uninitialized"
        },
        "Global_Language": {
          "agentEditable": false,
          "agentViewable": true,
          "displayName": "Customer Language",
          "global": true,
          "isSecure": false,
          "name": "Global_Language",
          "reportable": true,
          "secureKeyId": "",
          "secureKeyVersion": 0,
          "type": "STRING",
          "value": "en-US"
        },
        "Global_TestKey": {
          "agentEditable": true,
          "agentViewable": true,
          "displayName": "Global Test Key",
          "global": true,
          "isSecure": true,
          "name": "Global_TestKey",
          "reportable": false,
          "secureKeyId": "root",
          "secureKeyVersion": 3,
          "type": "STRING",
          "value": "eYXFa2Myvp7U0sIDvJDtKw==."
        },
        "TestKey": {
          "agentEditable": true,
          "agentViewable": true,
          "displayName": "Test Key 1",
          "global": false,
          "isSecure": false,
          "name": "TestKey",
          "reportable": false,
          "secureKeyId": "",
          "secureKeyVersion": 0,
          "type": "STRING",
          "value": "TestValue"
        },
        "TestSameerGlobal": {
          "agentEditable": true,
          "agentViewable": true,
          "displayName": "TestGlobal",
          "global": true,
          "isSecure": false,
          "name": "TestSameerGlobal",
          "reportable": false,
          "secureKeyId": "",
          "secureKeyVersion": 0,
          "type": "STRING",
          "value": "Sameer-value"
        },
        "ani": {
          "agentEditable": false,
          "agentViewable": true,
          "displayName": "ani",
          "global": false,
          "isSecure": false,
          "name": "ani",
          "reportable": false,
          "secureKeyId": "",
          "secureKeyVersion": 0,
          "type": "STRING",
          "value": "9487554325"
        },
        "dn": {
          "agentEditable": false,
          "agentViewable": true,
          "displayName": "dn",
          "global": false,
          "isSecure": false,
          "name": "dn",
          "reportable": false,
          "secureKeyId": "",
          "secureKeyVersion": 0,
          "type": "STRING",
          "value": "+15109024298"
        },
        "ronaTimeout": {
          "agentEditable": false,
          "agentViewable": true,
          "displayName": "ronaTimeout",
          "global": false,
          "isSecure": false,
          "name": "ronaTimeout",
          "reportable": false,
          "secureKeyId": "",
          "secureKeyVersion": 0,
          "type": "STRING",
          "value": "25"
        },
        "test3": {
          "agentEditable": true,
          "agentViewable": true,
          "displayName": "test3-new",
          "global": false,
          "isSecure": false,
          "name": "test3",
          "reportable": false,
          "secureKeyId": "",
          "secureKeyVersion": 0,
          "type": "INTEGER",
          "value": "0"
        },
        "virtualTeamName": {
          "agentEditable": false,
          "agentViewable": true,
          "displayName": "virtualTeamName",
          "global": false,
          "isSecure": false,
          "name": "virtualTeamName",
          "reportable": false,
          "secureKeyId": "",
          "secureKeyVersion": 0,
          "type": "STRING",
          "value": "Queue_MCM"
        }
      },
      "callAssociatedDetails": {
        "ani": "9487554325",
        "dn": "+15109024298",
        "ronaTimeout": "25",
        "virtualTeamName": "Queue_MCM"
      },
      "callFlowParams": {},
      "callProcessingDetails": {
        "CONSULTED_AGENT_QUEUE_ID": "0025a125-4d2c-4e1a-833d-909e95a389cc",
        "CONTINUE_RECORDING_ON_TRANSFER": "true",
        "EP_ID": "8befa99f-903e-4c33-8311-19666546b810",
        "QMgrName": "aqm",
        "QueueId": "0025a125-4d2c-4e1a-833d-909e95a389cc",
        "ani": "9487554325",
        "checkAgentAvailability": "false",
        "customerRegion": "intgus1",
        "dnis": "+15109024298",
        "fcDesktopView": "eNqVj0EKwjAQRe8y6xSsuuoFXAhump2ITHUWgXQSxzQgJXe3Ikg0irob/n8D/43gna9cJIFmOwJjT9AAsgEFEcVgZ6ml05TNIKkHcOSir/M+GgkDWk3Yb27JKzzPYXGM2vTkhlCAixzUdA5ruhTQEtJOgeFAgodgHFcemexfRt8W178uflJbWdeh3X8aXti100ly/3qrma7bbY9I",
        "fceRegisteredEvents": "",
        "flowTagId": "Latest",
        "isParked": "false",
        "mohFileName": "defaultmusic_on_hold.wav",
        "participantInviteTimeout": "false",
        "pauseDuration": "15",
        "pauseResumeEnabled": "true",
        "priority": "10",
        "queuedDestinationID": "0025a125-4d2c-4e1a-833d-909e95a389cc",
        "queuedTo": "Queue",
        "recordInProgress": "true",
        "recordingStarted": "true",
        "ronaTimeout": "25",
        "taskToBeSelfServiced": "false",
        "tenantId": "58f1a59e-245c-4536-9ee4-06560658e493",
        "virtualTeamName": "Queue_MCM",
        "vteamId": "0025a125-4d2c-4e1a-833d-909e95a389cc",
        "workflowId": "62a165a995fe092e845f4804",
        "workflowName": "FlowSameer"
      },
      "contactDirection": { "type": "INBOUND" },
      "createdTimestamp": 1728979793852,
      "currentVTeam": "0025a125-4d2c-4e1a-833d-909e95a389cc",
      "interactionId": "0b09cfec-feea-4ccf-a78a-b7b06d485be2",
      "isFcManaged": true,
      "isMediaForked": false,
      "isTerminated": false,
      "mainInteractionId": "0b09cfec-feea-4ccf-a78a-b7b06d485be2",
      "media": {
        "0b09cfec-feea-4ccf-a78a-b7b06d485be2": {
          "holdTimestamp": null,
          "isHold": false,
          "mType": "mainCall",
          "mediaMgr": "callmm",
          "mediaResourceId": "0b09cfec-feea-4ccf-a78a-b7b06d485be2",
          "mediaType": "telephony",
          "participants": ["9487554325", "3b05f0e9-48e5-40c9-8923-c50e9b0b22a7"]
        }
      },
      "mediaChannel": "telnyx",
      "mediaProperties": null,
      "mediaType": "telephony",
      "orgId": "58f1a59e-245c-4536-9ee4-06560658e493",
      "outboundType": null,
      "owner": "366f2a3a-dd91-482f-b57e-1abf93dda1f7",
      "parentInteractionId": "0b09cfec-feea-4ccf-a78a-b7b06d485be2",
      "participants": {
        "366f2a3a-dd91-482f-b57e-1abf93dda1f7": {
          "autoAnswerEnabled": true,
          "bnrDetails": null,
          "callerId": null,
          "channelId": "7be4ef42-e2d8-450c-b89c-84c966539fc0",
          "consultState": null,
          "consultTimestamp": null,
          "deviceCallId": null,
          "deviceId": null,
          "deviceType": null,
          "dn": "webrtc-366f2a3a-dd91-482f-b57e-1abf93dda1f7",
          "hasJoined": true,
          "hasLeft": true,
          "id": "366f2a3a-dd91-482f-b57e-1abf93dda1f7",
          "isConsulted": false,
          "isInPredial": false,
          "isOffered": true,
          "isWrapUp": true,
          "isWrappedUp": false,
          "joinTimestamp": 1728979798880,
          "lastUpdated": 1728979843589,
          "name": "vik intg3",
          "pType": "Agent",
          "queueId": "0025a125-4d2c-4e1a-833d-909e95a389cc",
          "queueMgrId": "aqm",
          "sessionId": "226f136d-c3ac-4440-98c8-e4ff2ada91b2",
          "siteId": "b302fbf4-28b8-4b56-add0-162e2464db89",
          "skillId": null,
          "skillName": null,
          "skills": [],
          "teamId": "bdd276cd-d051-4b80-bd6e-9fb9eec18b99",
          "teamName": "Team-Minions",
          "type": "Agent",
          "wrapUpTimestamp": 1728979843589
        },
        "3b05f0e9-48e5-40c9-8923-c50e9b0b22a7": {
          "autoAnswerEnabled": false,
          "bnrDetails": null,
          "callerId": null,
          "channelId": "83160396-10a1-460b-bc12-9d151050fb08",
          "consultState": null,
          "consultTimestamp": null,
          "deviceCallId": null,
          "deviceId": null,
          "deviceType": null,
          "dn": "webrtc-3b05f0e9-48e5-40c9-8923-c50e9b0b22a7",
          "hasJoined": true,
          "hasLeft": false,
          "id": "3b05f0e9-48e5-40c9-8923-c50e9b0b22a7",
          "isConsulted": false,
          "isInPredial": false,
          "isOffered": true,
          "isWrapUp": false,
          "isWrappedUp": false,
          "joinTimestamp": 1728979815616,
          "lastUpdated": 1728979815616,
          "name": "vik intg2",
          "pType": "Agent",
          "queueId": "0025a125-4d2c-4e1a-833d-909e95a389cc",
          "queueMgrId": "aqm",
          "sessionId": "b97fc378-c09d-43f0-8bf0-18294ab8d208",
          "siteId": "b302fbf4-28b8-4b56-add0-162e2464db89",
          "skillId": null,
          "skillName": null,
          "skills": [],
          "teamId": "bdd276cd-d051-4b80-bd6e-9fb9eec18b99",
          "teamName": "Team-Minions",
          "type": "Agent",
          "wrapUpTimestamp": null
        },
        "9487554325": {
          "callerId": null,
          "hasJoined": true,
          "hasLeft": false,
          "id": "9487554325",
          "isInPredial": false,
          "pType": "Customer",
          "type": "Customer"
        }
      },
      "previousVTeams": ["8befa99f-903e-4c33-8311-19666546b810"],
      "queuedTimestamp": null,
      "state": "connected",
      "workflowManager": null
    },
    "interactionId": "0b09cfec-feea-4ccf-a78a-b7b06d485be2",
    "orgId": "58f1a59e-245c-4536-9ee4-06560658e493",
    "queueMgr": "aqm",
    "trackingId": "05bcf437-d798-4c85-a70e-ce711de3c785",
    "type": "AgentConsultConferenceEnded"
  },
  "orgId": "58f1a59e-245c-4536-9ee4-06560658e493",
  "trackingId": "notifs_2a563687-b74d-4cbb-8679-94aa349c5a13",
  "type": "RoutingMessage"
}
```

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

### dropConferenceParticipant()

Removes a participant from an active conference.

**Note:** Only the primary agent on the conference can drop other participants from the conference.

**Example**

```javascript
await Desktop.agentContact.dropConferenceParticipant({
    interactionId: "706fa9d9-7561-4f57-b306-62bfaa5285db",
    data: {
        participantId: "66809250-2cb9-411a-8c63-8cab91bc4d1b"
    }
});

```

The following table lists the payload details:

| Name             | Type   | Description                                                          | Required |
| ---------------- | ------ | ---------------------------------------------------------------------- | -------- |
| interactionId    | String | Unique identifier for the user interaction.                            | Yes      |
| data             | Object | Options of the drop conference participant request.                   | Yes      |
| -->participantId | String | Unique identifier of the participant to remove from the conference.   | Yes      |

**Returns**
`{Object}` The object with the retrieved data.

**Note:** The `type` parameter value in the response payload depends on the success or failure of the method. If the method is successful, the value is `ParticipantLeftConference`; else, `ParticipantDropConferenceFailed`.

**Example Response**

```javascript
const dropConferenceParticipantResponse = {
  "data": {
    "droppedById": "b99c0871-b4da-4f36-9346-5bc1021e9a52",
    "eventTime": 1783673778329,
    "eventType": "RoutingMessage",
    "interaction": {
      "callAssociatedData": {
        // Nested fields omitted for brevity.
      },
      "callAssociatedDetails": {
        // Nested fields omitted for brevity.
      },
      "callFlowParams": {},
      "callProcessingDetails": {
        // Nested fields omitted for brevity.
      },
      "campaignOutboundType": null,
      "contactDirection": { "type": "INBOUND" },
      "createdTimestamp": 1783673737101,
      "currentVTeam": "a943338b-2920-48c1-a05e-bbe0a326c02a",
      "flowProperties": null,
      "interactionId": "706fa9d9-7561-4f57-b306-62bfaa5285db",
      "isFcManaged": true,
      "isMediaForked": false,
      "isTerminated": false,
      "mainInteractionId": "706fa9d9-7561-4f57-b306-62bfaa5285db",
      "media": {
        // Nested fields omitted for brevity.
      },
      "mediaChannel": "telnyx",
      "mediaProperties": null,
      "mediaType": "telephony",
      "orgId": "58f1a59e-245c-4536-9ee4-06560658e493",
      "outboundType": null,
      "owner": "b99c0871-b4da-4f36-9346-5bc1021e9a52",
      "parentInteractionId": "706fa9d9-7561-4f57-b306-62bfaa5285db",
      "participants": {
        // Nested fields omitted for brevity.
      },
      "previousVTeams": ["6941634b-c781-4d0a-8d70-bd2a2174dcd7"],
      "queuedTimestamp": null,
      "segments": {
        // Nested fields omitted for brevity.
      },
      "state": "connected",
      "workflowManager": null
    },
    "interactionId": "706fa9d9-7561-4f57-b306-62bfaa5285db",
    "leftParticipant": null,
    "orgId": "58f1a59e-245c-4536-9ee4-06560658e493",
    "participantId": "66809250-2cb9-411a-8c63-8cab91bc4d1b",
    "participantType": "Agent",
    "queueMgr": "aqm",
    "reason": null,
    "reasonCode": null,
    "trackingId": "d8593cf5-8a6e-4ab4-a09e-64df1ab08497",
    "type": "ParticipantLeftConference"
  },
  "orgId": "58f1a59e-245c-4536-9ee4-06560658e493",
  "trackingId": "notifs_705a6646-2185-4752-a5d6-1a7c1dd579ab",
  "type": "RoutingMessage"
};
```

## Verify Interaction Changes

Subscribe to the relevant [contact events](https://developer.webex.com/docs/desktop-contact-events) and check both success and failure events. Register listeners while the widget is mounted and remove them when it disconnects.

## Related Pages

- [Agent Desktop overview](https://developer.webex.com/docs/desktop)
- [Desktop SDK Reference](https://developer.webex.com/docs/desktop-sdk-reference)
