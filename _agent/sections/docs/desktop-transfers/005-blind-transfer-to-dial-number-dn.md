---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-transfers
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Agent Contact Methods
- blindTransfer()
- Blind Transfer to Dial Number(DN)
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/desktop-transfers). [Full Markdown](../../../../docs/desktop-transfers.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before You Begin](001-before-you-begin.md)

## Article introduction

Transfer interactions to agents, dial numbers, and queues with the Desktop SDK.

## Parent context

## Agent Contact Methods

These methods belong to `Desktop.agentContact`. Use the V2 method where the older method is marked for deprecation.

### blindTransfer()

**Caution:** This method will be deprecated in the future.

Initiates a blind transfer request. This method can be used to transfer a contact to an Agent or to a Dial Number.

## Selected section

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
