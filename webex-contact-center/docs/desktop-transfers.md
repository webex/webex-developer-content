---
type: Guide
title: Transfer Contacts
display_title: Transfer Contacts
canonical_url: https://developer.webex.com/docs/desktop-transfers
content_type: documentation
product_group:
- webex-contact-center
categories:
- webex-contact-center
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/desktop-transfers)

Transfer interactions to agents, dial numbers, and queues with the Desktop SDK.

## Before You Begin

Install and initialize the SDK as described in [Get Started with the Desktop SDK](https://developer.webex.com/docs/desktop-sdk-getting-started). Your widget must run inside Webex Contact Center Desktop.

## Agent Contact Methods

These methods belong to `Desktop.agentContact`. Use the V2 method where the older method is marked for deprecation.

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

### vTeamTransfer()

**Caution:** This method will be deprecated in the future.

Initiates a vTeam transfer request.

**Example**

```javascript
await Desktop.agentContact.vteamTransfer({
    interactionId: "dab1a2f0-bad0-11ea-8e7c-0d99ede2535a",
    data: {
        vteamId: "AXDiuOLjKin42Ov3QJXN",
        vteamType: "inboundqueue"
    }
});
```

**Payload type**

```typescript
type RequestPayload = {
    interactionId: string;
    data: Contact.vteamTransferPayLoad
}

type vteamTransferPayLoad = {
    vteamId: string;
    vteamType: string;
};
```

The following table lists the payload details:

| Name          | Type   | Description                                                                                                                                    | Required |
| ------------- | ------ | ---------------------------------------------------------------------------------------------------------------------------------------------- | -------- |
| interactionId | String | Unique identifier for the user interaction.                                                                                                    | Yes      |
| data          | Object | Options of the vTeam transfer request.                                                                                                         | Yes      |
| -->vteamId    | String | vTeam unique identifier.                                                                                                                       | Yes      |
| -->vteamType  | String | vTeam transfer type. <br> - inboundentrypoint: Indicates transfer to an entry point. <br> - inboundqueue: Indicates transfer to a queue. </br> | Yes      |

**Returns**
`{Object}` The object with the retrieved data.

**Note:** The `type` parameter value in the response payload depends on the success or failure of the method. If the method is successful, the value is `AgentVteamTransferred`; else, `AgentVteamTransferFailed`.

**Example Response**

```javascript
const vTeamTransferResponse = {
    "data": {
        "agentId": "7d12d9ea-e8e0-41ee-81bf-c11a685b64ed",
        "eventType": "RoutingMessage",
        "interaction": {
            "callAssociatedData": {
                "ani": {
                    "value": "janedoe@gmail.com"
                },
                "category": {
                    "value": "Sales"
                },
                "customerName": {
                    "value": "Jane Doe"
                },
                "dn": {
                    "value": "Desktop"
                },
                "entryPointId": {
                    "value": "AXCqFyz1G2pKap9PI-mW"
                },
                "guestId": {
                    "value": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS81NzNiODg1Mi1kZjM3LTRlODEtOGMxMi1mZjkyMTE3MmQ1NzY"
                },
                "mediaChannel": {
                    "value": "web"
                },
                "reason": {
                    "value": "Test"
                },
                "reasonCode": {
                    "value": "Sales"
                },
                "ronaTimeout": {
                    "value": "30"
                },
                "roomTitle": {
                    "value": "Help Jane Doe with Sales"
                },
                "taskToBeSelfServiced": {
                    "value": "false"
                },
                "templateId": {
                    "value": "b57990c0-5ec6-11ea-96ee-5df5aef56329"
                },
                "templateName": {
                    "value": "Desktop"
                },
                "virtualTeamName": {
                    "value": "Chat_Queue"
                }
            },
            "callAssociatedDetails": {
                "ani": "janedoe@gmail.com",
                "category": "Sales",
                "customerName": "Jane Doe",
                "dn": "Desktop",
                "entryPointId": "AXCqFyz1G2pKap9PI-mW",
                "guestId": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS81NzNiODg1Mi1kZjM3LTRlODEtOGMxMi1mZjkyMTE3MmQ1NzY",
                "mediaChannel": "web",
                "reason": "Test",
                "reasonCode": "Sales",
                "ronaTimeout": "30",
                "roomTitle": "Help Jane Doe with Sales",
                "taskToBeSelfServiced": "false",
                "templateId": "b57990c0-5ec6-11ea-96ee-5df5aef56329",
                "templateName": "Desktop",
                "virtualTeamName": "Chat_Queue"
            },
            "callFlowParams": {
                "Automation": {
                    "description": "(vteam, A valid VTeam.)",
                    "name": "Automation",
                    "qualifier": "vteam",
                    "value": "3270",
                    "valueDataType": "string"
                },
                "Debit": {
                    "description": "(vteam, A valid VTeam.)",
                    "name": "Debit",
                    "qualifier": "vteam",
                    "value": "3270",
                    "valueDataType": "string"
                },
                "Sales": {
                    "description": "(vteam, A valid VTeam.)",
                    "name": "Sales",
                    "qualifier": "vteam",
                    "value": "3270",
                    "valueDataType": "string"
                }
            },
            "callProcessingDetails": {
                "QMgrName": "aqm",
                "QueueId": "3270",
                "ani": "janedoe@gmail.com",
                "category": "Sales",
                "customerName": "Jane Doe",
                "dnis": "Desktop",
                "doNotRouteToAgents": "7d12d9ea-e8e0-41ee-81bf-c11a685b64ed",
                "entryPointId": "AXCqFyz1G2pKap9PI-mW",
                "guestId": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS81NzNiODg1Mi1kZjM3LTRlODEtOGMxMi1mZjkyMTE3MmQ1NzY",
                "mediaChannel": "web",
                "pauseDuration": "10",
                "pauseResumeEnabled": "true",
                "reason": "Test",
                "reasonCode": "Sales",
                "ronaTimeout": "30",
                "roomTitle": "Help Jane Doe with Sales",
                "taskToBeSelfServiced": "false",
                "templateId": "b57990c0-5ec6-11ea-96ee-5df5aef56329",
                "templateName": "Desktop",
                "tenantId": "133",
                "virtualTeamName": "Chat_Queue",
                "vteamId": "7178",
                "vteamType": "inboundqueue"
            },
            "contactDirection": {
                "type": "INBOUND"
            },
            "currentVTeam": "7178",
            "interactionId": "29bafa9c-40b5-11eb-8606-edd437f1b927",
            "isFcManaged": false,
            "isTerminated": false,
            "media": {
                "Y2lzY29zcGFyazovL3VzL1JPT00vMmNiMTMwMDAtNDBiNS0xMWViLWE4M2ItZWI4ZTQwMDk1MDk5": {
                    "holdTimestamp": null,
                    "isHold": false,
                    "mType": "mainCall",
                    "mediaMgr": "cmm",
                    "mediaResourceId": "Y2lzY29zcGFyazovL3VzL1JPT00vMmNiMTMwMDAtNDBiNS0xMWViLWE4M2ItZWI4ZTQwMDk1MDk5",
                    "mediaType": "chat",
                    "participants": ["janedoe@gmail.com", "7d12d9ea-e8e0-41ee-81bf-c11a685b64ed"]
                }
            },
            "mediaChannel": "web",
            "mediaType": "chat",
            "orgId": "f111e3af-1a45-42ef-9erf-4562354b8a25",
            "outboundType": null,
            "owner": null,
            "participants": {
                "7d12d9ea-e8e0-41ee-81bf-c11a685b64ed": {
                    "channelId": "ccbffa6f-4322-4e06-850f-e0ab2915f238",
                    "consultState": null,
                    "consultTimestamp": null,
                    "dn": "9997770110",
                    "hasJoined": true,
                    "id": "7d12d9ea-e8e0-41ee-81bf-c11a685b64ed",
                    "isConsulted": false,
                    "isWrapUp": true,
                    "joinTimestamp": 1608243279477,
                    "lastUpdated": 1608254153975,
                    "name": "FirstName LastName",
                    "pType": "Agent",
                    "queueId": "3270",
                    "queueMgrId": "aqm",
                    "sessionId": "b8c096ab-f9a0-49be-9efd-f8c78e1a7061",
                    "siteId": "473",
                    "teamId": "962",
                    "teamName": "Team X",
                    "type": "Agent",
                    "wrapUpTimestamp": 1608254153975
                },
                "janedoe@gmail.com": {
                    "id": "janedoe@gmail.com",
                    "pType": "Customer",
                    "type": "Customer"
                }
            },
            "previousVTeams": ["3270"],
            "state": "new"
        },
        "interactionId": "29bafa9c-40b5-11eb-8606-edd437f1b927",
        "orgId": "f111e3af-1a45-42ef-9erf-4562354b8a25",
        "queueMgr": "aqm",
        "trackingId": "91480930-40ce-11eb-840f-7f9e29c6b481",
        "type": "AgentVteamTransferred"
    },
    "orgId": "f111e3af-1a45-42ef-9erf-4562354b8a25", "trackingId": "notifs_08102baa-3437-4c6d-812c-db4ce8755ea0", "type": "RoutingMessage"
}
```

### blindTransfer()

**Caution:** This method will be deprecated in the future.

Initiates a blind transfer request. This method can be used to transfer a contact to an Agent or to a Dial Number.

#### Blind Transfer to Agent

**Example**

```javascript
await Desktop.agentContact.blindTransfer({
    interactionId: "08259a2b-bacf-11ea-bdd9-abbd16eaf1d5",
    data: {
        agentId: "f795f41f-3782-44fa-97a4-c8b4dc029477",
        destAgentId: "299b728a-d6f8-4934-8fad-577525c0b7fc",
        mediaType: "chat",
        destAgentTeamId: "964",
        destAgentDN: "9997770095",
        destSiteId: "472"
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
    agentId: string;
    destAgentId: string;
    mediaType: string;
    destAgentTeamId: string;
    destAgentDN: string;
    destSiteId: string;
};
```

The following table lists the payload details:

| Name               | Type   | Description                                                                                                                                                           | Required |
| ------------------ | ------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- |
| interactionId      | String | The unique ID represents the task that the user is currently working on. It is generated automatically during the creation of a new task.                                                                                                                           | Yes      |
| data               | Object | Options of the blind transfer request.                                                                                                                                | Yes      |
| -->agentId         | String | Unique identifier of the agent.                                                                                                                                       | Yes      |
| -->destAgentId     | String | Unique identifier of the destination agent. | Yes      |
| -->mediaType       | String | The media channel type such as chat.                                                                                                                                  | Yes      |
| -->destAgentTeamId | String | Unique identifier of the team to which the destination agent belongs.                                                                                                 | Yes      |
| -->destAgentDN     | String | The dial number of the destination agent.                                                                                                                             | Yes      |
| -->destSiteId      | String | Unique identifier of the destination site.                                                                                                                            | Yes      |

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
#### Blind Transfer to Dial Number(DN)

**Example**

```javascript
await Desktop.agentContact.blindTransfer({
    interactionId: "08259a2b-bacf-11ea-bdd9-abbd16eaf1d5",
    data: {
        destAgentId: "9997770095",
        mediaType: "telephony",
        destinationType: "DN"
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
    destAgentId: string;
    mediaType: string;
    destinationType: string;
};
```

The following table lists the payload details:

| Name               | Type   | Description                                                                                                                                                           | Required |
| ------------------ | ------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- |
| interactionId      | String | The unique ID represents the task that the user is currently working on. It is generated automatically during the creation of a new task.                                                                                                                           | Yes      |
| data               | Object | Payload for blind transfer to Dial Number request.                                                                                                                                | Yes      |
| -->mediaType       | String | The media channel type, for example, telephony.                                                                                                                                  | Yes      |
| -->destAgentId       | String | `destAgentId` refers to the Dial Number used for transfer.                                                                                                                                  | Yes      |
| -->destinationType         | String | The type of transfer request to be placed, for example, DN.                                                                                                                                  | Yes      |

**Returns**
`{Object}` The object with the retrieved data.

**Note:** The `type` parameter value in the response payload depends on the success or failure of the method. If the method is successful, the value is `AgentBlindTransferred`; else, `AgentBlindTransferFailedEvent`.

**Example Response**

```javascript
const blindTransferResponse = {
  "data": {
    "agentId": "aef2f5d3-7666-4e09-845e-5b019a9123f2",
    "destAgentId": "57xxxxxx3",
    "destinationType": "DN",
    "eventTime": 1727296398345,
    "eventType": "RoutingMessage",
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
          "value": "2024-09-25T20:32:32.014Z[UTC]"
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
          "value": "Test"
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
          "value": "zkK9t2ebro52iV6X19vmJA==."
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
        "TestGlobal": {
          "agentEditable": true,
          "agentViewable": true,
          "displayName": "TestGlobal",
          "global": true,
          "isSecure": false,
          "name": "TestGlobal",
          "reportable": false,
          "secureKeyId": "",
          "secureKeyVersion": 0,
          "type": "STRING",
          "value": "Test-value"
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
          "value": "94xxxxxxx5"
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
          "value": "94xxxxxxx5"
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
        "ani": "94xxxxxxx5",
        "dn": "+15xxxxxxxx8",
        "ronaTimeout": "25",
        "virtualTeamName": "Queue_MCM"
      },
      "callFlowParams": {},
      "callProcessingDetails": {
        "BLIND_TRANSFER_IN_PROGRESS": "true",
        "CONTINUE_RECORDING_ON_TRANSFER": "true",
        "EP_ID": "8befa99f-903e-4c33-8311-19666546b810",
        "QMgrName": "aqm",
        "QueueId": "0025a125-4d2c-4e1a-833d-909e95a389cc",
        "ROUTING_TYPE": "queueBasedRouting",
        "ani": "94xxxxxxx5",
        "checkAgentAvailability": "false",
        "customerRegion": "intgus1",
        "dnis": "+15xxxxxxxx8",
        "fcDesktopView": "eNqVj0EKwjAQRe8y6xSsuuoFXAhump2ITHUWgXQSxzQgJXe3Ikg0irob/n8D/43gna9cJIFmOwJjT9AAsgEFEcVgZ6ml05TNIKkHcOSir/M+GgkDWk3Yb27JKzzPYXGM2vTkhlCAixzUdA5ruhTQEtJOgeFAgodgHFcemexfRt8W178uflJbWdeh3X8aXti100ly/3qrma7bbY9I",
        "fceRegisteredEvents": "",
        "flowTagId": "Latest",
        "isParked": "false",
        "mohFileName": "defaultmusic_on_hold.wav",
        "pauseDuration": "15",
        "pauseResumeEnabled": "true",
        "priority": "10",
        "queuedDestinationID": "0025a125-4d2c-4e1a-833d-909e95a389cc",
        "queuedTo": "Queue",
        "recordingStarted": "true",
        "ronaTimeout": "25",
        "taskToBeSelfServiced": "false",
        "tenantId": "58f1a59e-245c-4536-9ee4-06560658e493",
        "virtualTeamName": "Queue_MCM",
        "vteamId": "0025a125-4d2c-4e1a-833d-909e95a389cc",
        "workflowId": "62a165a995fe092e845f4804",
        "workflowName": "FlowTest"
      },
      "contactDirection": { "type": "INBOUND" },
      "createdTimestamp": 1727296351593,
      "currentVTeam": "0025a125-4d2c-4e1a-833d-909e95a389cc",
      "interactionId": "04b00173-9a60-4115-aaa2-9993c3496951",
      "isFcManaged": true,
      "isMediaForked": false,
      "isTerminated": false,
      "mainInteractionId": "04b00173-9a60-4115-aaa2-9993c3496951",
      "media": {
        "04b00173-9a60-4115-aaa2-9993c3496951": {
          "holdTimestamp": null,
          "isHold": false,
          "mType": "mainCall",
          "mediaMgr": "callmm",
          "mediaResourceId": "04b00173-9a60-4115-aaa2-9993c3496951",
          "mediaType": "telephony",
          "participants": ["94xxxxxxx5", "aef2f5d3-7666-4e09-845e-5b019a9123f2"]
        }
      },
      "mediaChannel": "telnyx",
      "mediaProperties": null,
      "mediaType": "telephony",
      "orgId": "58f1a59e-245c-4536-9ee4-06560658e493",
      "outboundType": null,
      "owner": null,
      "parentInteractionId": "04b00173-9a60-4115-aaa2-9993c3496951",
      "participants": {
        "5xxxxxxxx8": {
          "callerId": null,
          "hasLeft": false,
          "id": "5xxxxxxxx8",
          "isInPredial": false,
          "pType": "DN",
          "type": "DN"
        },
        "94xxxxxxx5": {
          "callerId": null,
          "hasJoined": true,
          "hasLeft": false,
          "id": "94xxxxxxx5",
          "isInPredial": false,
          "pType": "Customer",
          "type": "Customer"
        },
        "aef2f5d3-7666-4e09-845e-5b019a9123f2": {
          "autoAnswerEnabled": false,
          "bnrDetails": null,
          "callerId": null,
          "channelId": "9c04e312-8e14-43c4-a7e4-2c20f12b623e",
          "consultState": null,
          "consultTimestamp": null,
          "dn": "webrtc-aef2f5d3-7666-4e09-845e-5b019a9123f2",
          "hasJoined": true,
          "hasLeft": true,
          "id": "aef2f5d3-7666-4e09-845e-5b019a9123f2",
          "isConsulted": false,
          "isInPredial": false,
          "isOffered": true,
          "isWrapUp": false,
          "isWrappedUp": false,
          "joinTimestamp": 1727296375103,
          "lastUpdated": 1727296375103,
          "name": "Test User",
          "pType": "Agent",
          "queueId": "0025a125-4d2c-4e1a-833d-909e95a389cc",
          "queueMgrId": "aqm",
          "sessionId": "5cf402c0-f814-40d1-86fc-b0b756e4baf9",
          "siteId": "b302fbf4-28b8-4b56-add0-162e2464db89",
          "skillId": null,
          "skillName": null,
          "skills": [],
          "teamId": "bdd276cd-d051-4b80-bd6e-9fb9eec18b99",
          "teamName": "Team-Test",
          "type": "Agent",
          "wrapUpTimestamp": null
        }
      },
      "previousVTeams": ["8befa99f-903e-4c33-8311-19666546b810"],
      "queuedTimestamp": null,
      "state": "new",
      "workflowManager": null
    },
    "interactionId": "04b00173-9a60-4115-aaa2-9993c3496951",
    "mediaResourceId": "04b00173-9a60-4115-aaa2-9993c3496951",
    "orgId": "58f1a59e-245c-4536-9ee4-06560658e493",
    "queueMgr": "aqm",
    "trackingId": "be82db7f-04d6-4b03-a1df-655366e6c142",
    "type": "AgentBlindTransferred"
  },
  "orgId": "58f1a59e-245c-4536-9ee4-06560658e493",
  "trackingId": "notifs_4d2aca4a-409d-460d-a4be-e81973178919",
  "type": "RoutingMessage"
};
```

### consultTransfer()

**Caution:** This method will be deprecated in the future.

Initiates a consult transfer request.

**Example**

```javascript
await Desktop.agentContact.consultTransfer({
    interactionId: "5c3d487a-874b-447d-b5f2-ce1f626301f5",
    data: {
        agentId: "43bfcdef-5551-45b1-a8f9-a0b33e66e3fe",
        destAgentId: "f795f41f-3782-44fa-97a4-c8b4dc029477",
        mediaType: "telephony",
        mediaResourceId: "b102ed10-fac2-4f8e-bece-1c2da6ba6dd8",
        destinationType: "Agent",
    }
});
```

**Payload type**

```typescript
type RequestPayload = {
    interactionId: string;data: Contact.consultTransferPayLoad
}

type consultTransferPayLoad = {
    agentId ?: string | undefined;
    destAgentId: string;
    mediaType: string;
    mediaResourceId: string;
    destinationType ?: string | undefined;
};
```

The following table lists the payload details:

| Name               | Type   | Description                                                                                         | Required |
| ------------------ | ------ | --------------------------------------------------------------------------------------------------- | -------- |
| interactionId      | String | Unique identifier for the user interaction.                                                         | Yes      |
| data               | Object | Options of the consult transfer request.                                                            | Yes      |
| -->agentId         | String | Unique identifier of the agent.                                                                     | Yes      |
| -->destAgentId     | String | Unique identifier of the consult transfer request destination agent.                                | Yes      |
| -->mediaType       | String | The media channel type such as telephony.                                                           | Yes      |
| -->mediaResourceId | String | Unique identifier of the media resource.                                                            | Yes      |
| -->destinationType | String | The type of consult transfer request to be placed. The destination type can be Agent, Queue, or DN. | Yes      |

**Returns**
`{Object}` The object with the retrieved data.

**Note:** The `type` parameter value in the response payload depends on the success or failure of the method. If the method is successful, the value is `AgentConsultTransferred`; else, `AgentConsultTransferFailed`.

**Example Response**

```javascript
const consultTransferResponse = {
  data: {
    agentId: "ff7dbe19-fa3f-4c63-8a1c-04dcffef8e4f",
    consultMediaResourceId: "fd0af60c-3250-46c3-96f8-1921f6ecf170",
    destAgentId: "9b036d89-930c-4187-a5bd-5dbb1439fe41",
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
          holdTimestamp: null,
          isHold: false,
          mType: "mainCall",
          mediaMgr: "vmm",
          mediaResourceId: "1277da79-dc49-439c-ab72-f00453a1ff71",
          mediaType: "telephony",
          participants: ["**********", "9b036d89-930c-4187-a5bd-5dbb1439fe41"]
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
          consultState: null,
          consultTimestamp: null,
          dn: "**********",
          hasJoined: true,
          id: "9b036d89-930c-4187-a5bd-5dbb1439fe41",
          isConsulted: true,
          isWrapUp: false,
          joinTimestamp: 1612429549032,
          lastUpdated: 1612429549032,
          name: "qaus1-gt-user1 qaus1-gt-user1",
          pType: "Agent",
          queueId: "1336",
          queueMgrId: "aqm",
          sessionId: "90896c91-0f77-4bc6-aec3-488a34ca88d3",
          siteId: "205",
          teamId: "598",
          teamName: "Sales",
          type: "Agent",
          wrapUpTimestamp: null
        },
        "ff7dbe19-fa3f-4c63-8a1c-04dcffef8e4f": {
          channelId: "fb704337-71c3-4802-a03b-84a2d18eeaa0",
          consultState: "consulting",
          consultTimestamp: 1612429549052,
          dn: "**********",
          hasJoined: true,
          id: "ff7dbe19-fa3f-4c63-8a1c-04dcffef8e4f",
          isConsulted: false,
          isWrapUp: false,
          joinTimestamp: 1612429537991,
          lastUpdated: 1612429537991,
          name: "qaus1-gt-user2 q",
          pType: "Agent",
          queueId: "1336",
          queueMgrId: "aqm",
          sessionId: "57323f8b-9460-45fa-aaf6-4ca51c327af8",
          siteId: "205",
          teamId: "598",
          teamName: "Sales",
          type: "Agent",
          wrapUpTimestamp: null
        }
      },
      previousVTeams: ["AW6h1AVRrZSGni185x28"],
      state: "connected",
      workflowManager: null
    },
    interactionId: "1277da79-dc49-439c-ab72-f00453a1ff71",
    mediaResourceId: "1277da79-dc49-439c-ab72-f00453a1ff71",
    orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
    queueMgr: "aqm",
    trackingId: "05b38615-5bdc-4e1d-8efe-60ea1c70fd5c",
    transferredMediaResourceId: "1277da79-dc49-439c-ab72-f00453a1ff71",
    type: "AgentConsultTransferred"
  },
  orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
  trackingId: "notifs_3464be63-83e7-4b2d-94d5-a63fddc108d5",
  type: "RoutingMessage"
};
```

### consultTransferV2()

Initiates a consult transfer request.

**Example**

```javascript
await Desktop.agentContact.consultTransferV2({
    interactionId: "5c3d487a-874b-447d-b5f2-ce1f626301f5",
    data: {
        to: "43bfcdef-5551-45b1-a8f9-a0b33e66e3fe",
        destinationType: "agent"
    }
});
```

**Payload type**

```typescript
type RequestPayload = {
    interactionId: string;data: Contact.transferV2Payload
}

type transferV2Payload = {
    to: string;
    destinationType: string;
};
```

The following table lists the payload details:

| Name               | Type   | Description                                                                                         | Required |
| ------------------ | ------ | --------------------------------------------------------------------------------------------------- | -------- |
| interactionId      | String | Unique identifier for the user interaction.                                                         | Yes      |
| data               | Object | Options of the consult transfer request.                                                            | Yes      |
| -->to  | String | Destination identifier or value for the selected destination type.                                                         | Yes      |
| -->destinationType | String | The type of consult transfer request to be placed. The destination type can be agent, queue, entryPoint or dialNumber. | Yes      |

**Returns**
`{Object}` The object with the retrieved data.

**Note:** The `type` parameter value in the response payload depends on the success or failure of the method. If the method is successful, the value is `AgentConsultTransferred`; else, `AgentConsultTransferFailed`.

**Example Response**

```javascript
const consultTransferResponse = {
  data: {
    agentId: "ff7dbe19-fa3f-4c63-8a1c-04dcffef8e4f",
    consultMediaResourceId: "fd0af60c-3250-46c3-96f8-1921f6ecf170",
    destAgentId: "9b036d89-930c-4187-a5bd-5dbb1439fe41",
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
          holdTimestamp: null,
          isHold: false,
          mType: "mainCall",
          mediaMgr: "vmm",
          mediaResourceId: "1277da79-dc49-439c-ab72-f00453a1ff71",
          mediaType: "telephony",
          participants: ["**********", "9b036d89-930c-4187-a5bd-5dbb1439fe41"]
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
          consultState: null,
          consultTimestamp: null,
          dn: "**********",
          hasJoined: true,
          id: "9b036d89-930c-4187-a5bd-5dbb1439fe41",
          isConsulted: true,
          isWrapUp: false,
          joinTimestamp: 1612429549032,
          lastUpdated: 1612429549032,
          name: "qaus1-gt-user1 qaus1-gt-user1",
          pType: "Agent",
          queueId: "1336",
          queueMgrId: "aqm",
          sessionId: "90896c91-0f77-4bc6-aec3-488a34ca88d3",
          siteId: "205",
          teamId: "598",
          teamName: "Sales",
          type: "Agent",
          wrapUpTimestamp: null
        },
        "ff7dbe19-fa3f-4c63-8a1c-04dcffef8e4f": {
          channelId: "fb704337-71c3-4802-a03b-84a2d18eeaa0",
          consultState: "consulting",
          consultTimestamp: 1612429549052,
          dn: "**********",
          hasJoined: true,
          id: "ff7dbe19-fa3f-4c63-8a1c-04dcffef8e4f",
          isConsulted: false,
          isWrapUp: false,
          joinTimestamp: 1612429537991,
          lastUpdated: 1612429537991,
          name: "qaus1-gt-user2 q",
          pType: "Agent",
          queueId: "1336",
          queueMgrId: "aqm",
          sessionId: "57323f8b-9460-45fa-aaf6-4ca51c327af8",
          siteId: "205",
          teamId: "598",
          teamName: "Sales",
          type: "Agent",
          wrapUpTimestamp: null
        }
      },
      previousVTeams: ["AW6h1AVRrZSGni185x28"],
      state: "connected",
      workflowManager: null
    },
    interactionId: "1277da79-dc49-439c-ab72-f00453a1ff71",
    mediaResourceId: "1277da79-dc49-439c-ab72-f00453a1ff71",
    orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
    queueMgr: "aqm",
    trackingId: "05b38615-5bdc-4e1d-8efe-60ea1c70fd5c",
    transferredMediaResourceId: "1277da79-dc49-439c-ab72-f00453a1ff71",
    type: "AgentConsultTransferred"
  },
  orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
  trackingId: "notifs_3464be63-83e7-4b2d-94d5-a63fddc108d5",
  type: "RoutingMessage"
};
```

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

### vTeamTransferV2()

Initiates a vTeam transfer request.

**Example**

```javascript
await Desktop.agentContact.vteamTransferV2({
    interactionId: "dab1a2f0-bad0-11ea-8e7c-0d99ede2535a",
    data: {
        to: "AXDiuOLjKin42Ov3QJXN",
        destinationType: "queue"
    }
});
```

**Payload type**

```typescript
type RequestPayload = {
    interactionId: string;
    data: Contact.vteamTransferV2PayLoad
}

type vteamTransferV2PayLoad = {
    to: string;
    destinationType: string;
};
```

The following table lists the payload details:

| Name          | Type   | Description                                                                                                                                    | Required |
| ------------- | ------ | ---------------------------------------------------------------------------------------------------------------------------------------------- | -------- |
| interactionId | String | Unique identifier for the user interaction.                                                                                                    | Yes      |
| data          | Object | Options of the vTeam transfer request.                                                                                                         | Yes      |
| -->to    | String | vTeam unique identifier.                                                                                                                       | Yes      |
| -->destinationType  | String | vTeam transfer type. The user can transfer to another user in the team(agent), queue(queue), dial number(dialNumber), entry point(entrypointDialNumber). | Yes      |

**Returns**
`{Object}` The object with the retrieved data.

**Note:** The `type` parameter value in the response payload depends on the success or failure of the method. If the method is successful, the value is `AgentVteamTransferred`; else, `AgentVteamTransferFailed`.

**Example Response**

```javascript
const vTeamTransferResponse = {
    "data": {
        "agentId": "7d12d9ea-e8e0-41ee-81bf-c11a685b64ed",
        "eventType": "RoutingMessage",
        "interaction": {
            "callAssociatedData": {
                "ani": {
                    "value": "janedoe@gmail.com"
                },
                "category": {
                    "value": "Sales"
                },
                "customerName": {
                    "value": "Jane Doe"
                },
                "dn": {
                    "value": "Desktop"
                },
                "entryPointId": {
                    "value": "AXCqFyz1G2pKap9PI-mW"
                },
                "guestId": {
                    "value": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS81NzNiODg1Mi1kZjM3LTRlODEtOGMxMi1mZjkyMTE3MmQ1NzY"
                },
                "mediaChannel": {
                    "value": "web"
                },
                "reason": {
                    "value": "Test"
                },
                "reasonCode": {
                    "value": "Sales"
                },
                "ronaTimeout": {
                    "value": "30"
                },
                "roomTitle": {
                    "value": "Help Jane Doe with Sales"
                },
                "taskToBeSelfServiced": {
                    "value": "false"
                },
                "templateId": {
                    "value": "b57990c0-5ec6-11ea-96ee-5df5aef56329"
                },
                "templateName": {
                    "value": "Desktop"
                },
                "virtualTeamName": {
                    "value": "Chat_Queue"
                }
            },
            "callAssociatedDetails": {
                "ani": "janedoe@gmail.com",
                "category": "Sales",
                "customerName": "Jane Doe",
                "dn": "Desktop",
                "entryPointId": "AXCqFyz1G2pKap9PI-mW",
                "guestId": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS81NzNiODg1Mi1kZjM3LTRlODEtOGMxMi1mZjkyMTE3MmQ1NzY",
                "mediaChannel": "web",
                "reason": "Test",
                "reasonCode": "Sales",
                "ronaTimeout": "30",
                "roomTitle": "Help Jane Doe with Sales",
                "taskToBeSelfServiced": "false",
                "templateId": "b57990c0-5ec6-11ea-96ee-5df5aef56329",
                "templateName": "Desktop",
                "virtualTeamName": "Chat_Queue"
            },
            "callFlowParams": {
                "Automation": {
                    "description": "(vteam, A valid VTeam.)",
                    "name": "Automation",
                    "qualifier": "vteam",
                    "value": "3270",
                    "valueDataType": "string"
                },
                "Debit": {
                    "description": "(vteam, A valid VTeam.)",
                    "name": "Debit",
                    "qualifier": "vteam",
                    "value": "3270",
                    "valueDataType": "string"
                },
                "Sales": {
                    "description": "(vteam, A valid VTeam.)",
                    "name": "Sales",
                    "qualifier": "vteam",
                    "value": "3270",
                    "valueDataType": "string"
                }
            },
            "callProcessingDetails": {
                "QMgrName": "aqm",
                "QueueId": "3270",
                "ani": "janedoe@gmail.com",
                "category": "Sales",
                "customerName": "Jane Doe",
                "dnis": "Desktop",
                "doNotRouteToAgents": "7d12d9ea-e8e0-41ee-81bf-c11a685b64ed",
                "entryPointId": "AXCqFyz1G2pKap9PI-mW",
                "guestId": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS81NzNiODg1Mi1kZjM3LTRlODEtOGMxMi1mZjkyMTE3MmQ1NzY",
                "mediaChannel": "web",
                "pauseDuration": "10",
                "pauseResumeEnabled": "true",
                "reason": "Test",
                "reasonCode": "Sales",
                "ronaTimeout": "30",
                "roomTitle": "Help Jane Doe with Sales",
                "taskToBeSelfServiced": "false",
                "templateId": "b57990c0-5ec6-11ea-96ee-5df5aef56329",
                "templateName": "Desktop",
                "tenantId": "133",
                "virtualTeamName": "Chat_Queue",
                "vteamId": "7178",
                "vteamType": "inboundqueue"
            },
            "contactDirection": {
                "type": "INBOUND"
            },
            "currentVTeam": "7178",
            "interactionId": "29bafa9c-40b5-11eb-8606-edd437f1b927",
            "isFcManaged": false,
            "isTerminated": false,
            "media": {
                "Y2lzY29zcGFyazovL3VzL1JPT00vMmNiMTMwMDAtNDBiNS0xMWViLWE4M2ItZWI4ZTQwMDk1MDk5": {
                    "holdTimestamp": null,
                    "isHold": false,
                    "mType": "mainCall",
                    "mediaMgr": "cmm",
                    "mediaResourceId": "Y2lzY29zcGFyazovL3VzL1JPT00vMmNiMTMwMDAtNDBiNS0xMWViLWE4M2ItZWI4ZTQwMDk1MDk5",
                    "mediaType": "chat",
                    "participants": ["janedoe@gmail.com", "7d12d9ea-e8e0-41ee-81bf-c11a685b64ed"]
                }
            },
            "mediaChannel": "web",
            "mediaType": "chat",
            "orgId": "f111e3af-1a45-42ef-9erf-4562354b8a25",
            "outboundType": null,
            "owner": null,
            "participants": {
                "7d12d9ea-e8e0-41ee-81bf-c11a685b64ed": {
                    "channelId": "ccbffa6f-4322-4e06-850f-e0ab2915f238",
                    "consultState": null,
                    "consultTimestamp": null,
                    "dn": "9997770110",
                    "hasJoined": true,
                    "id": "7d12d9ea-e8e0-41ee-81bf-c11a685b64ed",
                    "isConsulted": false,
                    "isWrapUp": true,
                    "joinTimestamp": 1608243279477,
                    "lastUpdated": 1608254153975,
                    "name": "FirstName LastName",
                    "pType": "Agent",
                    "queueId": "3270",
                    "queueMgrId": "aqm",
                    "sessionId": "b8c096ab-f9a0-49be-9efd-f8c78e1a7061",
                    "siteId": "473",
                    "teamId": "962",
                    "teamName": "Team X",
                    "type": "Agent",
                    "wrapUpTimestamp": 1608254153975
                },
                "janedoe@gmail.com": {
                    "id": "janedoe@gmail.com",
                    "pType": "Customer",
                    "type": "Customer"
                }
            },
            "previousVTeams": ["3270"],
            "state": "new"
        },
        "interactionId": "29bafa9c-40b5-11eb-8606-edd437f1b927",
        "orgId": "f111e3af-1a45-42ef-9erf-4562354b8a25",
        "queueMgr": "aqm",
        "trackingId": "91480930-40ce-11eb-840f-7f9e29c6b481",
        "type": "AgentVteamTransferred"
    }
}
```

## Verify Interaction Changes

Subscribe to the relevant [contact events](https://developer.webex.com/docs/desktop-contact-events) and check both success and failure events. Register listeners while the widget is mounted and remove them when it disconnects.

## Related Pages

- [Agent Desktop overview](https://developer.webex.com/docs/desktop)
- [Desktop SDK Reference](https://developer.webex.com/docs/desktop-sdk-reference)
