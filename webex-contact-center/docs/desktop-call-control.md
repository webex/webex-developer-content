---
type: Guide
title: Tasks and Call Control
display_title: Tasks and Call Control
canonical_url: https://developer.webex.com/docs/desktop-call-control
content_type: documentation
product_group:
- webex-contact-center
categories:
- webex-contact-center
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/desktop-call-control)

Retrieve tasks and control interactions, WebRTC calls, and call recording from Desktop widgets.

## Before You Begin

Install and initialize the SDK as described in [Get Started with the Desktop SDK](https://developer.webex.com/docs/desktop-sdk-getting-started). Your widget must run inside Webex Contact Center Desktop.

## Desktop Actions

The `Desktop.actions` module retrieves data and performs actions for Desktop widgets.

### addCustomTask()

Adds a new custom task within your widget. The task appears in the Desktop task list.

**Note:** To keep the list of tasks up to date within your widget, you must add event listeners and subscribe to asynchronous events. The events signify new tasks being assigned to an agent. For more information, see [Asynchronous Events](https://developer.webex.com/docs/desktop-contact-events#asynchronous-events).

**Example**

```javascript
const contactPayload = {
        mediaResourceId: "49bcf26b-ec75-4351-89fa-55d54682c20c",
        eventType: "RoutingMessage",
        agentId: "16839506-7c48-4a71-ba1b-d585e5d37607",
        trackingId: "354deeae-c98a-4a8c-9e04-e56e129fdb9f",
        interaction: {
            isFcManaged: false,
            isTerminated: false,
            mediaType: "telephony",
            previousVTeams: ["AXCZ0YCAXrf9I0XFBI7b"],
            state: "connected",
            currentVTeam: "3268",
            participants: {
                "+19997770096": {
                    id: "+19997770096",
                    pType: "Customer",
                    type: "Customer"
                },
                "aad323de-32d8-48c9-af6b-b68dfbabfe20": {
                    name: "uuip-agent2",
                    pType: "Agent",
                    teamName: "Team X",
                    lastUpdated: 1597681728863,
                    teamId: "962",
                    joinTimestamp: 1597681728863,
                    isConsulted: false,
                    hasJoined: true,
                    consultTimestamp: null,
                    dn: "9997770194",
                    queueId: "3268",
                    id: "16839506-7c48-4a71-ba1b-d585e5d37607",
                    sessionId: "319d8e83-2a75-4ef3-9cb8-1c845edb15a0",
                    consultState: null,
                    queueMgrId: "aqm",
                    siteId: "473",
                    type: "Agent",
                    channelId: "ab8b3603-84a7-4f61-b987-9044b4d69cf2",
                    wrapUpTimestamp: null,
                    isWrapUp: false
                }
            },
            interactionId: "49bcf26b-ec75-4351-89fa-55d54682c20c",
            orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
            callAssociatedData: {
                customerName: {
                    value: "test",
                    name: "r",
                    agentEditable: false,
                    type: "s",
                    displayName: "d"
                }
            },
            callAssociatedDetails: {
                virtualTeamName: "Queue - Telephony",
                ani: "+19997770096",
                ronaTimeout: "30",
                dn: "+12147659000",
                pathId: " StartCall PlayDone out out out",
                IvrPath: " EOI",
                subject: "",
                toAddress: "",
                inReplyTo: "",
                customerName: "",
                ccAddress: "",
                entryPointId: "",
                accountId: "",
                reasonCode: "",
                reason: "",
                references: "",
                contentType: "",
                date: "",
                replyToAddress: "",
                fromAddress: "",
                messageId: "",
                from: "",
                threadId: "",
                bccAddress: "",
                queueType: "",
                dnis: "",
                category: "",
                sourceNumber: "",
                sourcePage: "",
                appUser: "",
                customerNumber: ""
            },
            callProcessingDetails: {
                QMgrName: "aqm",
                pauseResumeEnabled: "true",
                taskToBeSelfServiced: "false",
                ani: "+19997770096",
                recordInProgress: "true",
                pauseDuration: "10",
                dnis: "+12147659000",
                tenantId: "133",
                QueueId: "3268",
                vteamId: "3268",
                jscriptId: "AXCZ4c3mjkwgAuS7vSIU",
                customerName: "",
                virtualTeamName: "Queue - Telephony",
                ronaTimeout: "30",
                category: "",
                reason: "",
                sourceNumber: "",
                sourcePage: "",
                appUser: "",
                customerNumber: "",
                reasonCode: "",
                IvrPath: " EOI",
                pathId: " StartCall PlayDone out out out",
                fromAddress: ""
            },
            media: {
                "49bcf26b-ec75-4351-89fa-55d54682c20c": {
                    mediaResourceId: "49bcf26b-ec75-4351-89fa-55d54682c20c",
                    mediaType: "telephony",
                    mediaMgr: "vmm",
                    participants: ["+19997770096", "16839506-7c48-4a71-ba1b-d585e5d37607"],
                    mType: "mainCall",
                    isHold: false,
                    holdTimestamp: null
                }
            },
            owner: "16839506-7c48-4a71-ba1b-d585e5d37607",
            mediaChannel: "broadcloud",
            contactDirection: {
                type: "INBOUND"
            },
            callFlowParams: {
                Play2: {
                    name: "Play2",
                    qualifier: "",
                    description: "(A valid text.)",
                    valueDataType: "string",
                    value: "Welcome to Agent Team Space"
                },
                Queue3: {
                    name: "Queue3",
                    qualifier: "vteam",
                    description: "(vteam, A valid VTeam.)",
                    valueDataType: "string",
                    value: "3268"
                }
            }
        },
        interactionId: "49bcf26b-ec75-4351-89fa-55d54682c20c",
        orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
        queueMgr: "aqm",
        type: "AgentContactAssigned",
        destAgentId: "16839506-7c48-4a71-ba1b-d585e5d37607",
        consultMediaResourceId: "",
        owner: "",
        isConferencing: false
};
Desktop.actions.addCustomTask(contactPayload);
// => Add custom task object in Desktop store
```

### getTaskMap()

Retrieves the full list of tasks that are assigned to an agent at a given time.

**Example**

```javascript
const currentTaskMap = await Desktop.actions.getTaskMap();
// => Get current task map from Desktop store
```

Returns
`{Map}` A list of results.

**Example Response**

```text
Desktop Store TaskMap:
    Map(1) {
        "851a8e81-6150-11eb-9a47-f1ca3756d4bd" => {
            …}, "eed4b53a-614f-11eb-9a47-8be6439707ee" => {
            …}
    }
    [
        [Entries]
    ] {
        "851a8e81-6150-11eb-9a47-f1ca3756d4bd" => Object
    }
key: "851a8e81-6150-11eb-9a47-f1ca3756d4bd"
value:
    agentId: "7c867aa9-ec768-341a-b767-e5hd6ae7g701"
eventType: "RoutingMessage"
interaction: {
    callAssociatedData: {
        …},
    callAssociatedDetails: {
        …},
    callFlowParams: {
        …},
    callProcessingDetails: {
        …},
    contactDirection: {
        …},
    …
}
interactionId: "851a8e81-6150-11eb-9a47-f1ca3756d4bd"
mediaResourceId: "4D44FF32-A585-4DD8-8422-4920FC97066A@cisco.com"
orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25"
queueMgr: "aqm"
trackingId: "69773a10-6163-11eb-9fb9-8dadf7aee433"
type: "AgentContactAssigned"
```

### acceptWebRtcCall()

Accepts an incoming WebRTC call. This method allows agents to answer WebRTC-based voice calls routed through the contact center.

**Example**

```javascript
await Desktop.actions.acceptWebRtcCall();
// => Accept the incoming WebRTC call
```

Returns
 The response will be similar to the "AgentContactAssigned" event.

### declineWebRtcCall()

Declines an incoming WebRTC call. This method allows agents to reject WebRTC-based voice calls that are being offered.

**Example**

```javascript
await Desktop.actions.declineWebRtcCall();
// => Decline the incoming WebRTC call
```


**Example Response**

```json
{
    "data": {
        "agentId": "4f91ee74-9747-4c97-ae25-c2a753f2edb1",
        "agentSessionId": "89ad50c4-99f5-4c83-afb4-4f238d93b664",
        "eventTime": 1758824113184,
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
                    "value": "2025-09-25T18:15:02.534Z[UTC]"
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
                    "value": "+15109024297"
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
                "dn": "+15109024297",
                "ronaTimeout": "25",
                "virtualTeamName": "Queue_MCM"
            },
            "callFlowParams": {},
            "callProcessingDetails": {
                "EP_ID": "6941634b-c781-4d0a-8d70-bd2a2174dcd7",
                "QMgrName": "aqm",
                "QueueId": "0025a125-4d2c-4e1a-833d-909e95a389cc",
                "ROUTING_TYPE": "queueBasedRouting",
                "ani": "9487554325",
                "checkAgentAvailability": "false",
                "contactAssignmentType": "ACD",
                "customerRegion": "intgus1",
                "dnis": "+15109024297",
                "fcDesktopView": "eNp9kE0LgzAMhv9LzgpzHxev206DXeZtDIk2h0JsXa3CEP/7Oiaj2tFLDnmfJOQZodVtqgcykN9HUNgQ5IBKQgIDGokV042erreBKfkBQgV55ueDNLZHLgib66ezhrc+XFBnL/QKoJ0PWQeVy5IFE/v12rOQAq3LA/QA0yMBqSwZrK3UKm1REfsWOqp7Q2WlNcdtzKCgWjbIcTMz6w7HpSgi/rJxL/EvF0KOyHxC+9/F9AYS3a1l",
                "fceRegisteredEvents": "ContactLastAgentRemoved",
                "flowTagId": "Latest",
                "mohFileName": "defaultmusic_on_hold.wav",
                "participantInviteTimeout": "false",
                "priority": "10",
                "queuedDestinationID": "0025a125-4d2c-4e1a-833d-909e95a389cc",
                "queuedTo": "Queue",
                "ronaTimeout": "25",
                "taskToBeSelfServiced": "false",
                "tenantId": "58f1a59e-245c-4536-9ee4-06560658e493",
                "virtualTeamName": "Queue_MCM",
                "vteamId": "0025a125-4d2c-4e1a-833d-909e95a389cc",
                "workflowId": "62a165a995fe092e845f4804",
                "workflowName": "FlowSameer"
            },
            "contactDirection": {
                "type": "INBOUND"
            },
            "createdTimestamp": 1758824102098,
            "currentVTeam": "0025a125-4d2c-4e1a-833d-909e95a389cc",
            "flowProperties": null,
            "interactionId": "3bfe5b7b-3c99-40f5-9d30-08c81060b3a8",
            "isFcManaged": true,
            "isMediaForked": false,
            "isTerminated": false,
            "mainInteractionId": "3bfe5b7b-3c99-40f5-9d30-08c81060b3a8",
            "media": {
                "3bfe5b7b-3c99-40f5-9d30-08c81060b3a8": {
                    "holdTimestamp": null,
                    "isHold": false,
                    "mType": "mainCall",
                    "mediaMgr": "callmm",
                    "mediaResourceId": "3bfe5b7b-3c99-40f5-9d30-08c81060b3a8",
                    "mediaType": "telephony",
                    "participants": [
                        "9487554325"
                    ]
                }
            },
            "mediaChannel": "telnyx",
            "mediaProperties": null,
            "mediaType": "telephony",
            "orgId": "58f1a59e-245c-4536-9ee4-06560658e493",
            "outboundType": null,
            "owner": null,
            "parentInteractionId": "3bfe5b7b-3c99-40f5-9d30-08c81060b3a8",
            "participants": {
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
            "previousVTeams": [
                "6941634b-c781-4d0a-8d70-bd2a2174dcd7"
            ],
            "queuedTimestamp": 1758824103297,
            "state": "new",
            "workflowManager": null
        },
        "interactionId": "3bfe5b7b-3c99-40f5-9d30-08c81060b3a8",
        "mediaResourceId": "3bfe5b7b-3c99-40f5-9d30-08c81060b3a8",
        "orgId": "58f1a59e-245c-4536-9ee4-06560658e493",
        "queueMgr": "aqm",
        "reason": "USER_DECLINED",
        "reasonCode": 156,
        "trackingId": "e544a8e5-2c4f-4a1d-8fb2-66fe3443883f",
        "type": "AgentContactAssignFailed"
    },
    "orgId": "58f1a59e-245c-4536-9ee4-06560658e493",
    "trackingId": "notifs_9cc2b4a2-6f87-487b-9e03-f2686b1eb17e",
    "type": "RoutingMessage"
}
```

### toggleMuteUnmuteWebRtcCall()

Toggles the mute/unmute state for an active WebRTC call. This method switches between muted and unmuted states for the agent's microphone during an ongoing WebRTC call session.

**Example**

```javascript
await Desktop.actions.toggleMuteUnmuteWebRtcCall();
// => Toggle mute/unmute state for the current WebRTC call
```

### sendDtmf(dtmfData)

Sends Dual-Tone Multi-Frequency (DTMF) signals during an active call. DTMF tones are used to interact with Interactive Voice Response (IVR) systems, access voicemail systems, or navigate automated phone menus. Each tone corresponds to a specific digit or symbol on a telephone keypad.

**Example**

```javascript
// Send a single digit
await Desktop.agentContact.sendDtmf("5");

// Send multiple digits for a PIN or extension
await Desktop.agentContact.sendDtmf("1234");

// Send special characters
await Desktop.agentContact.sendDtmf("*");
await Desktop.agentContact.sendDtmf("#");

// Send a sequence for navigating an IVR menu
await Desktop.agentContact.sendDtmf("2*9876#");
```

**Parameters**

| Name     | Type   | Description                                                                                           | Required |
| -------- | ------ | ----------------------------------------------------------------------------------------------------- | -------- |
| dtmfData | String | The DTMF tone(s) to send. Valid characters: 0-9, *, #. Can be a single character or a sequence.     | Yes      |

## Agent Contact Methods

These methods belong to `Desktop.agentContact`. Use the V2 method where the older method is marked for deprecation.

### accept()

**Caution:** This method will be deprecated in the future.

Accepts an incoming task.

**Note:** This method works only for non-voice tasks and isn't applicable for voice contacts.

**Example**

```javascript
await Desktop.agentContact.accept({
    interactionId: "c837e6f7-699a-4736-bb82-03a6d58bb7f3"
});
```

The following table lists the payload details:

| Name          | Type   | Description                                 | Required |
| ------------- | ------ | ------------------------------------------- | -------- |
| interactionId | String | Unique identifier for the user interaction. | Yes      |

**Returns**

`{Object}` The value that corresponds to the task.

**Note:** The `type` parameter value in the response payload depends on the success or failure of the method. If the method is successful, the value is `AgentContactAssigned`; else, `AgentContactAssignFailed`.

**Example Response**

```javascript
const acceptResponse = {
  data: {
    agentId: "7d12d9ea-e8e0-41ee-81bf-c11a685b64ed",
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
            "Y2lzY29zcGFyazovL3VzL1BFT1BMRS83ZjA3YjJmMC1jNTMyLTQ5MDktYTkzNi0yYTA3MTVmZGIwMTA"
        },
        mediaChannel: {
          value: "web"
        },
        reason: {
          value: "Test"
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
          "Y2lzY29zcGFyazovL3VzL1BFT1BMRS83ZjA3YjJmMC1jNTMyLTQ5MDktYTkzNi0yYTA3MTVmZGIwMTA",
        mediaChannel: "web",
        reason: "Test",
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
          "Y2lzY29zcGFyazovL3VzL1BFT1BMRS83ZjA3YjJmMC1jNTMyLTQ5MDktYTkzNi0yYTA3MTVmZGIwMTA",
        mediaChannel: "web",
        reason: "Test",
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
      interactionId: "59dbbca6-4194-11eb-881c-253923a967e0",
      isFcManaged: false,
      isTerminated: false,
      media: {
        Y2lzY29zcGFyazovL3VzL1JPT00vNjVjOWVlYjAtNDE5NC0xMWViLWE1N2QtZWY2N2MwZTMyYmFh:
          {
            holdTimestamp: null,
            isHold: false,
            mType: "mainCall",
            mediaMgr: "cmm",
            mediaResourceId:
              "Y2lzY29zcGFyazovL3VzL1JPT00vNjVjOWVlYjAtNDE5NC0xMWViLWE1N2QtZWY2N2MwZTMyYmFh",
            mediaType: "chat",
            participants: [
              "janedoe@gmail.com",
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
          channelId: "bff9350a-9d2a-489a-a8d5-d9dacea4b692",
          consultState: null,
          consultTimestamp: null,
          dn: "9997770110",
          hasJoined: true,
          id: "7d12d9ea-e8e0-41ee-81bf-c11a685b64ed",
          isConsulted: false,
          isWrapUp: false,
          joinTimestamp: 1608339210824,
          lastUpdated: 1608339210824,
          name: "uuip-agent4 uuip-agent4",
          pType: "Agent",
          queueId: "3270",
          queueMgrId: "aqm",
          sessionId: "102d2096-bcc0-45bb-a583-a02f6c188071",
          siteId: "473",
          teamId: "1940",
          teamName: "Medical Help",
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
      state: "connected"
    },
    interactionId: "59dbbca6-4194-11eb-881c-253923a967e0",
    mediaResourceId:
      "Y2lzY29zcGFyazovL3VzL1JPT00vNjVjOWVlYjAtNDE5NC0xMWViLWE1N2QtZWY2N2MwZTMyYmFh",
    orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
    queueMgr: "aqm",
    trackingId: "9c9b97e0-4194-11eb-b819-7b8dd50ee0cd",
    type: "AgentContactAssigned"
  },
  orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
  trackingId: "notifs_02db68c8-a5db-4028-95bb-1aebd6f87609",
  type: "RoutingMessage"
};
```

### end()

**Caution:** This method will be deprecated in the future.

Ends an interaction for a specific task.
**Note:** The end call feature is enabled using the `isEndCallEnabled` payload. For more information, see [Agent State Information Module](https://developer.webex.com/docs/desktop-agent-state#agent-state-information-module).

**Example**

```javascript
await Desktop.agentContact.end({
    interactionId: "c837e6f7-699a-4736-bb82-03a6d58bb7f3"
});
```

The following table lists the payload details:

| Name          | Type   | Description                                 | Required |
| ------------- | ------ | ------------------------------------------- | -------- |
| interactionId | String | Unique identifier for the user interaction. | Yes      |

**Returns**

`{Object}` The value that corresponds to the task.

**Note:** The `type` parameter value in the response payload depends on the success or failure of the method. If the method is successful, the value is `AgentWrapup` or `ContactEnded`; else, `ContactEndFailed`.

**Example Response**

```javascript
const endResponse = {
  data: {
    agentsPendingWrapUp: ["7d12d9ea-e8e0-41ee-81bf-c11a685b64ed"],
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
          value: "Test"
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
        reason: "Please help",
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
        reason: "Please help",
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
      interactionId: "a66d05ab-40ab-11eb-b59a-7d3326b3ffc1",
      isFcManaged: false,
      isTerminated: true,
      media: {},
      mediaChannel: "web",
      mediaType: "chat",
      orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
      outboundType: null,
      owner: "7d12d9ea-e8e0-41ee-81bf-c11a685b64ed",
      participants: {
        "7d12d9ea-e8e0-41ee-81bf-c11a685b64ed": {
          channelId: "ff0a5296-8aa2-483b-8c50-577fedb1bfde",
          consultState: null,
          consultTimestamp: null,
          dn: "9997770110",
          hasJoined: true,
          id: "7d12d9ea-e8e0-41ee-81bf-c11a685b64ed",
          isConsulted: false,
          isWrapUp: false,
          joinTimestamp: 1608239195992,
          lastUpdated: 1608239195992,
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
        "janedoe@gmail.com": {
          id: "janedoe@gmail.com",
          pType: "Customer",
          type: "Customer"
        }
      },
      previousVTeams: [],
      state: "connected"
    },
    interactionId: "a66d05ab-40ab-11eb-b59a-7d3326b3ffc1",
    mediaResourceId:
      "Y2lzY29zcGFyazovL3VzL1JPT00vYWEzNTA5YzAtNDBhYi0xMWViLWE1N2QtZWY2N2MwZTMyYmFh",
    orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
    queueMgr: "aqm",
    trackingId: "4eb68870-40ac-11eb-8866-d7ef6ff89aa6",
    type: "ContactEnded"
  },
  orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
  trackingId: "notifs_3cda2c34-1410-4476-9c5c-5d779a615b8a",
  type: "RoutingMessage"
};
```

### wrapup()

**Caution:** This method will be deprecated in the future.

Wraps up work for a task. Wrap up reason is applied after the task has been ended either by the agent or by the customer. A wrap up is essential and is the last step in an agent's flow of handling tasks.

**Example**

```javascript
await Desktop.agentContact.wrapup({
    interactionId: "dab1a2f0-bad0-11ea-8e7c-0d99ede2535a",
    data: {
        wrapUpReason: "Sales",
        auxCodeId: "AXUH3oN12eV-WekpnDpl",
        isAutoWrapup: false,
    }
});
```

**Payload type**

```typescript
type RequestPayload = {
    interactionId: string;data: Contact.WrapupPayLoad
};
```

The following table lists the payload details:

| Name            | Type    | Description                                                                                                                                | Required |
| --------------- | ------- | ------------------------------------------------------------------------------------------------------------------------------------------ | -------- |
| interactionId   | String  | Unique identifier for the user interaction.                                                                                                | Yes      |
| data            | Object  | Options of the wrap up.                                                                                                                    | Yes      |
| -->wrapUpReason | String  | Every wrap up reason will have an unique auxillary code. Use this field to specify the reason for wrapping up the call, maximum length 128 characters.                                                                        | Yes      |
| -->auxCodeId    | String  | Auxiliary codes are status codes which an agent can select in Webex Contact Center Agent Desktop. They are of two types: Idle and Wrap-Up codes, and every agent profile must have one of each for the agent to use.  Wrap-up codes indicate the result of customer contacts, such as successful resolution or escalation of the contact. Creating and managing auxiliary codes requires an administrator role and the appropriate cjp:config_write or cjp:config_read scopes, maximum length 36 characters.                                                                                                      | Yes      |
| -->isAutoWrapup | Boolean | Determines whether the auto wrap up is enabled or not.<br><br>- True—The auto warp up is enabled.<br>- False—The auto warp up is disabled. | Yes      |

**Returns**
`{Object}` The object with the retrieved data.

**Note:** The `type` parameter value in the response payload depends on the success or failure of the method. If the method is successful, the value is `AgentWrappedUp`; else, `AgentWrapupFailed`.

**Example Response**

```javascript
const wrapUpResponse = {
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
                "vteamId": "AXCqFyz1G2pKap9PI-mW"
            },
            "contactDirection": {
                "type": "INBOUND"
            },
            "currentVTeam": "3270",
            "interactionId": "a66d05ab-40ab-11eb-b59a-7d3326b3ffc1",
            "isFcManaged": false,
            "isTerminated": true,
            "media": {},
            "mediaChannel": "web",
            "mediaType": "chat",
            "orgId": "f111e3af-1a45-42ef-9erf-4562354b8a25",
            "outboundType": null,
            "owner": "7d12d9ea-e8e0-41ee-81bf-c11a685b64ed",
            "participants": {
                "janedoe@gmail.com": {
                    "id": "janedoe@gmail.com",
                    "pType": "Customer",
                    "type": "Customer"
                }
            },
            "previousVTeams": [],
            "state": "connected"
        },
        "interactionId": "a66d05ab-40ab-11eb-b59a-7d3326b3ffc1",
        "orgId": "f111e3af-1a45-42ef-9erf-4562354b8a25",
        "queueMgr": "aqm",
        "trackingId": "5272a610-40ac-11eb-8866-d7ef6ff89aa6",
        "type": "AgentWrappedUp",
        "wrapUpAuxCodeId": "0"
    },
    "orgId": "f111e3af-1a45-42ef-9erf-4562354b8a25",
    "trackingId": "notifs_b5e0ebb7-fd1d-479f-8663-81a64030cee6",
    "type": "RoutingMessage"
}
```

### hold()

Places a voice call on hold.

**Example**

```javascript
await Desktop.agentContact.hold({
    interactionId: "c837e6f7-699a-4736-bb82-03a6d58bb7f3",
    data: {
        mediaResourceId: "c837e6f7-699a-4736-bb82-03a6d58bb7f3"
    }
});

```

**Payload type**

```typescript
type HoldPayload = {
    interactionId: string;
    data: { mediaResourceId: string };
};
```

The following table lists the payload details:

| Name               | Type   | Description                                 | Required |
| ------------------ | ------ | ------------------------------------------- | -------- |
| interactionId      | String | Unique identifier for the user interaction. | Yes      |
| data               | Object | Options to place the voice call on hold.    | Yes      |
| -->mediaResourceId | String | Unique identifier of the media resource.    | Yes      |

**Returns**
`{Object}` The object with the retrieved data.

**Note:** The `type` parameter value in the response payload depends on the success or failure of the method. If the method is successful, the value is `AgentContactHeld`; else, `AgentContactHoldFailed`.

**Example Response**

```javascript
const holdResponse = {
  data: {
    agentId: "7c867aa9-ec768-341a-b767-e5hd6ae7g701",
    destAgentId: null,
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
          holdTimestamp: 1612355834441,
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
    mediaResourceId: "1dd08726-bca5-4ce8-9b51-b20dca8ab154",
    orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
    queueMgr: "aqm",
    trackingId: "3768264d-8588-465f-9ee6-0c25418ea9f7",
    type: "AgentContactHeld"
  },
  orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
  trackingId: "notifs_8e8cabb7-6d5a-460d-9b8b-ecfad96448b3",
  type: "RoutingMessage"
};
```

### unHold()

Resumes a voice call that is placed on hold.

**Example**

```javascript
await Desktop.agentContact.unHold({
    interactionId: "c837e6f7-699a-4736-bb82-03a6d58bb7f3",
    data: {
        mediaResourceId: "c837e6f7-699a-4736-bb82-03a6d58bb7f3"
    }
});
```

**Payload type**

```typescript
type RequestPayload = {
    interactionId: string;data: {
        mediaResourceId: string
    }
};
```

The following table lists the payload details:

| Name               | Type   | Description                                              | Required |
| ------------------ | ------ | -------------------------------------------------------- | -------- |
| interactionId      | String | Unique identifier for the user interaction.              | Yes      |
| data               | Object | Options to resume the voice call that is placed on hold. | Yes      |
| -->mediaResourceId | String | Unique identifier of the media resource.                 | Yes      |

**Returns**
`{Object}` The object with the retrieved data.

**Note:** The `type` parameter value in the response payload depends on the success or failure of the method. If the method is successful, the value is `AgentContactUnheld`; else, `AgentContactUnHoldFailed`.

**Example Response**

```javascript
const unHoldResponse = {
  data: {
    agentId: "7c867aa9-ec768-341a-b767-e5hd6ae7g701",
    destAgentId: null,
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
          holdTimestamp: null,
          isHold: false,
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
    mediaResourceId: "1dd08726-bca5-4ce8-9b51-b20dca8ab154",
    orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
    queueMgr: "aqm",
    trackingId: "a5152cc8-004a-4e4c-b5d8-c9fc947f1e57",
    type: "AgentContactUnheld"
  },
  orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
  trackingId: "notifs_85f4d943-8e95-49c9-92c4-66047d526506",
  type: "RoutingMessage"
};
```

### pauseRecording()

**Caution:** This method will be deprecated in the future.

Pauses a call recording while obtaining sensitive information such as credit card information from the customer.

When configured by the administrator, voice calls are recorded for various reasons. When an agent handles sensitive customer information, the agent might want to pause the recording. The Pause/Resume functionality is available on the Desktop through the Interaction Control pane. You can access the Pause/Resume functionality from your widget also.

**Example**

```javascript
await Desktop.agentContact.pauseRecording({
    interactionId: "c837e6f7-699a-4736-bb82-03a6d58bb7f3"
});
// Pausing a recording for telephony task
```

The following table lists the payload details:

| Name          | Type   | Description                                 | Required |
| ------------- | ------ | ------------------------------------------- | -------- |
| interactionId | String | Unique identifier for the user interaction. | Yes      |

**Returns**
`{Object}` The object with the retrieved data.

**Note:** The `type` parameter value in the response payload depends on the success or failure of the method. If the method is successful, the value is `ContactRecordingPaused`; else, `ContactRecordingPauseFailed`.

**Example Response**

```javascript
const pauseRecordingResponse = {
  data: {
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
        isPaused: "true",
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
          holdTimestamp: null,
          isHold: false,
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
    trackingId: "b031f6d7-63a3-49d9-b377-e848bce41bd3",
    type: "ContactRecordingPaused"
  },
  orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
  trackingId: "notifs_52a00992-95e8-438c-ac44-8302da18d252",
  type: "RoutingMessage"
};
```

### resumeRecording()

**Caution:** This method will be deprecated in the future.

Resumes a voice call recording that is paused.

**Example**

```javascript
await Desktop.agentContact.resumeRecording({
    interactionId: "c837e6f7-699a-4736-bb82-03a6d58bb7f3",
    data: {
        autoResumed: true
    }
});
// Resuming recording for telephony task
```

**Payload type**

```typescript
type RequestPayload = {
    interactionId: string;data: {
        autoResumed: boolean
    }
};
```

The following table lists the payload details:

| Name           | Type    | Description                                                                                                                                                                                                                                                      | Required |
| -------------- | ------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- |
| interactionId  | String  | Unique identifier for the user interaction.                                                                                                                                                                                                                      | Yes      |
| data           | Object  | Options to resume a voice call recording that is paused.                                                                                                                                                                                                         | Yes      |
| -->autoResumed | Boolean | Determines whether the paused call must be resumed manually.<br>True—Voice call to be resumed automatically after the specified time is lapsed.<br>False—User to take action on the paused voice call based on the button defined. For example, Start Recording. | Yes      |

**Returns**
`{Object}` The object with the retrieved data.

**Note:** The `type` parameter value in the response payload depends on the success or failure of the method. If the method is successful, the value is `ContactRecordingResumed`; else, `ContactRecordingResumeFailed`.

**Example Response**

```javascript
const resumeRecordingResponse = {
  data: {
    autoResumed: true,
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
          holdTimestamp: null,
          isHold: false,
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
    trackingId: "9cf5bfc4-d120-4330-9996-039a9937c52c",
    type: "ContactRecordingResumed"
  },
  orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
  trackingId: "notifs_c04510a0-140a-439c-9ab4-68b6fdf6ea2e",
  type: "RoutingMessage"
};
```

### acceptV2()
Accepts an incoming task.

**Note:** This method works only for non-voice tasks and isn't applicable for voice contacts.

**Example**

```javascript
await Desktop.agentContact.acceptV2({
    interactionId: "c837e6f7-699a-4736-bb82-03a6d58bb7f3"
});
```

The following table lists the payload details:

| Name          | Type   | Description                                 | Required |
| ------------- | ------ | ------------------------------------------- | -------- |
| interactionId | String | Unique identifier for the user interaction. | Yes      |

**Returns**

`{Object}` The value that corresponds to the task.

**Note:** The `type` parameter value in the response payload depends on the success or failure of the method. If the method is successful, the value is `AgentContactAssigned`; else, `AgentContactAssignFailed`.

**Example Response**

```javascript
const acceptResponse = {
  data: {
    agentId: "7d12d9ea-e8e0-41ee-81bf-c11a685b64ed",
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
            "Y2lzY29zcGFyazovL3VzL1BFT1BMRS83ZjA3YjJmMC1jNTMyLTQ5MDktYTkzNi0yYTA3MTVmZGIwMTA"
        },
        mediaChannel: {
          value: "web"
        },
        reason: {
          value: "Test"
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
          "Y2lzY29zcGFyazovL3VzL1BFT1BMRS83ZjA3YjJmMC1jNTMyLTQ5MDktYTkzNi0yYTA3MTVmZGIwMTA",
        mediaChannel: "web",
        reason: "Test",
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
          "Y2lzY29zcGFyazovL3VzL1BFT1BMRS83ZjA3YjJmMC1jNTMyLTQ5MDktYTkzNi0yYTA3MTVmZGIwMTA",
        mediaChannel: "web",
        reason: "Test",
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
      interactionId: "59dbbca6-4194-11eb-881c-253923a967e0",
      isFcManaged: false,
      isTerminated: false,
      media: {
        Y2lzY29zcGFyazovL3VzL1JPT00vNjVjOWVlYjAtNDE5NC0xMWViLWE1N2QtZWY2N2MwZTMyYmFh:
          {
            holdTimestamp: null,
            isHold: false,
            mType: "mainCall",
            mediaMgr: "cmm",
            mediaResourceId:
              "Y2lzY29zcGFyazovL3VzL1JPT00vNjVjOWVlYjAtNDE5NC0xMWViLWE1N2QtZWY2N2MwZTMyYmFh",
            mediaType: "chat",
            participants: [
              "janedoe@gmail.com",
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
          channelId: "bff9350a-9d2a-489a-a8d5-d9dacea4b692",
          consultState: null,
          consultTimestamp: null,
          dn: "9997770110",
          hasJoined: true,
          id: "7d12d9ea-e8e0-41ee-81bf-c11a685b64ed",
          isConsulted: false,
          isWrapUp: false,
          joinTimestamp: 1608339210824,
          lastUpdated: 1608339210824,
          name: "uuip-agent4 uuip-agent4",
          pType: "Agent",
          queueId: "3270",
          queueMgrId: "aqm",
          sessionId: "102d2096-bcc0-45bb-a583-a02f6c188071",
          siteId: "473",
          teamId: "1940",
          teamName: "Medical Help",
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
      state: "connected"
    },
    interactionId: "59dbbca6-4194-11eb-881c-253923a967e0",
    mediaResourceId:
      "Y2lzY29zcGFyazovL3VzL1JPT00vNjVjOWVlYjAtNDE5NC0xMWViLWE1N2QtZWY2N2MwZTMyYmFh",
    orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
    queueMgr: "aqm",
    trackingId: "9c9b97e0-4194-11eb-b819-7b8dd50ee0cd",
    type: "AgentContactAssigned"
  },
  orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
  trackingId: "notifs_02db68c8-a5db-4028-95bb-1aebd6f87609",
  type: "RoutingMessage"
};
```

### endV2()

Ends an interaction for a specific task.
**Note:** The end call feature is enabled using the `isEndCallEnabled` payload. For more information, see [Agent State Information Module](https://developer.webex.com/docs/desktop-agent-state#agent-state-information-module).

**Example**

```javascript
await Desktop.agentContact.endV2({
    interactionId: "c837e6f7-699a-4736-bb82-03a6d58bb7f3",
    isEndingFromNonPrimary: true
});
```

The following table lists the payload details:

| Name          | Type   | Description                                 | Required |
| ------------- | ------ | ------------------------------------------- | -------- |
| interactionId | String | Unique identifier for the user interaction. | Yes      |
| isEndingFromNonPrimary | Boolean | Determines whether the end requested from non primary agent. | Yes      |

**Returns**

`{Object}` The value that corresponds to the task.

**Note:** The `type` parameter value in the response payload depends on the success or failure of the method. If the method is successful, the value is `AgentWrapup` or `ContactEnded`; else, `ContactEndFailed`.

**Example Response**

```javascript
const endResponse = {
  data: {
    agentsPendingWrapUp: ["7d12d9ea-e8e0-41ee-81bf-c11a685b64ed"],
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
          value: "Test"
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
        reason: "Please help",
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
        reason: "Please help",
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
      interactionId: "a66d05ab-40ab-11eb-b59a-7d3326b3ffc1",
      isFcManaged: false,
      isTerminated: true,
      media: {},
      mediaChannel: "web",
      mediaType: "chat",
      orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
      outboundType: null,
      owner: "7d12d9ea-e8e0-41ee-81bf-c11a685b64ed",
      participants: {
        "7d12d9ea-e8e0-41ee-81bf-c11a685b64ed": {
          channelId: "ff0a5296-8aa2-483b-8c50-577fedb1bfde",
          consultState: null,
          consultTimestamp: null,
          dn: "9997770110",
          hasJoined: true,
          id: "7d12d9ea-e8e0-41ee-81bf-c11a685b64ed",
          isConsulted: false,
          isWrapUp: false,
          joinTimestamp: 1608239195992,
          lastUpdated: 1608239195992,
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
        "janedoe@gmail.com": {
          id: "janedoe@gmail.com",
          pType: "Customer",
          type: "Customer"
        }
      },
      previousVTeams: [],
      state: "connected"
    },
    interactionId: "a66d05ab-40ab-11eb-b59a-7d3326b3ffc1",
    mediaResourceId:
      "Y2lzY29zcGFyazovL3VzL1JPT00vYWEzNTA5YzAtNDBhYi0xMWViLWE1N2QtZWY2N2MwZTMyYmFh",
    orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
    queueMgr: "aqm",
    trackingId: "4eb68870-40ac-11eb-8866-d7ef6ff89aa6",
    type: "ContactEnded"
  },
  orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
  trackingId: "notifs_3cda2c34-1410-4476-9c5c-5d779a615b8a",
  type: "RoutingMessage"
};
```

### cancelTaskV2()
Ends an interaction for a specific task.
**Note:** The end call feature is enabled using the `isEndCallEnabled` payload. For more information, see [Agent State Information Module](https://developer.webex.com/docs/desktop-agent-state#agent-state-information-module).

**Example**

```javascript
await Desktop.agentContact.cancelTaskV2({
    interactionId: "c837e6f7-699a-4736-bb82-03a6d58bb7f3"
});
```

The following table lists the payload details:

| Name          | Type   | Description                                 | Required |
| ------------- | ------ | ------------------------------------------- | -------- |
| interactionId | String | Unique identifier for the user interaction. | Yes      |

**Returns**

`{Object}` The value that corresponds to the task.

**Note:** The `type` parameter value in the response payload depends on the success or failure of the method. If the method is successful, the value is `ContactEnded`; else, `ContactEndFailed`.

**Example Response**

```javascript
const endResponse = {
  data: {
    agentsPendingWrapUp: ["7d12d9ea-e8e0-41ee-81bf-c11a685b64ed"],
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
          value: "Test"
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
        reason: "Please help",
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
        reason: "Please help",
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
      interactionId: "a66d05ab-40ab-11eb-b59a-7d3326b3ffc1",
      isFcManaged: false,
      isTerminated: true,
      media: {},
      mediaChannel: "web",
      mediaType: "chat",
      orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
      outboundType: null,
      owner: "7d12d9ea-e8e0-41ee-81bf-c11a685b64ed",
      participants: {
        "7d12d9ea-e8e0-41ee-81bf-c11a685b64ed": {
          channelId: "ff0a5296-8aa2-483b-8c50-577fedb1bfde",
          consultState: null,
          consultTimestamp: null,
          dn: "9997770110",
          hasJoined: true,
          id: "7d12d9ea-e8e0-41ee-81bf-c11a685b64ed",
          isConsulted: false,
          isWrapUp: false,
          joinTimestamp: 1608239195992,
          lastUpdated: 1608239195992,
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
        "janedoe@gmail.com": {
          id: "janedoe@gmail.com",
          pType: "Customer",
          type: "Customer"
        }
      },
      previousVTeams: [],
      state: "connected"
    },
    interactionId: "a66d05ab-40ab-11eb-b59a-7d3326b3ffc1",
    mediaResourceId:
      "Y2lzY29zcGFyazovL3VzL1JPT00vYWEzNTA5YzAtNDBhYi0xMWViLWE1N2QtZWY2N2MwZTMyYmFh",
    orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
    queueMgr: "aqm",
    trackingId: "4eb68870-40ac-11eb-8866-d7ef6ff89aa6",
    type: "ContactEnded"
  },
  orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
  trackingId: "notifs_3cda2c34-1410-4476-9c5c-5d779a615b8a",
  type: "RoutingMessage"
};
```

### pauseRecordingV2()

Pauses a call recording while obtaining sensitive information such as credit card information from the customer.

When configured by the administrator, voice calls are recorded for various reasons. When an agent handles sensitive customer information, the agent might want to pause the recording. The Pause/Resume functionality is available on the Desktop through the Interaction Control pane. You can access the Pause/Resume functionality from your widget also.

**Example**

```javascript
await Desktop.agentContact.pauseRecordingV2({
    interactionId: "c837e6f7-699a-4736-bb82-03a6d58bb7f3"
});
// Pausing a recording for telephony task
```

The following table lists the payload details:

| Name          | Type   | Description                                 | Required |
| ------------- | ------ | ------------------------------------------- | -------- |
| interactionId | String | Unique identifier for the user interaction. | Yes      |

**Returns**
`{Object}` The object with the retrieved data.

**Note:** The `type` parameter value in the response payload depends on the success or failure of the method. If the method is successful, the value is `ContactRecordingPaused`; else, `ContactRecordingPauseFailed`.

**Example Response**

```javascript
const pauseRecordingResponse = {
  data: {
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
        isPaused: "true",
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
          holdTimestamp: null,
          isHold: false,
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
    trackingId: "b031f6d7-63a3-49d9-b377-e848bce41bd3",
    type: "ContactRecordingPaused"
  },
  orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
  trackingId: "notifs_52a00992-95e8-438c-ac44-8302da18d252",
  type: "RoutingMessage"
};
```

### resumeRecordingV2()

Resumes a voice call recording that is paused.

**Example**

```javascript
await Desktop.agentContact.resumeRecordingV2({
    interactionId: "c837e6f7-699a-4736-bb82-03a6d58bb7f3",
    data: {
        autoResumed: true
    }
});
// Resuming recording for telephony task
```

**Payload type**

```typescript
type RequestPayload = {
    interactionId: string;data: {
        autoResumed: boolean
    }
};
```

The following table lists the payload details:

| Name           | Type    | Description                                                                                                                                                                                                                                                      | Required |
| -------------- | ------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- |
| interactionId  | String  | Unique identifier for the user interaction.                                                                                                                                                                                                                      | Yes      |
| data           | Object  | Options to resume a voice call recording that is paused.                                                                                                                                                                                                         | Yes      |
| -->autoResumed | Boolean | Determines whether the paused call must be resumed manually.<br>True—Voice call to be resumed automatically after the specified time is lapsed.<br>False—User to take action on the paused voice call based on the button defined. For example, Start Recording. | Yes      |

**Returns**
`{Object}` The object with the retrieved data.

**Note:** The `type` parameter value in the response payload depends on the success or failure of the method. If the method is successful, the value is `ContactRecordingResumed`; else, `ContactRecordingResumeFailed`.

**Example Response**

```javascript
const resumeRecordingResponse = {
  data: {
    autoResumed: true,
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
          holdTimestamp: null,
          isHold: false,
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
    trackingId: "9cf5bfc4-d120-4330-9996-039a9937c52c",
    type: "ContactRecordingResumed"
  },
  orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
  trackingId: "notifs_c04510a0-140a-439c-9ab4-68b6fdf6ea2e",
  type: "RoutingMessage"
};
```

### wrapupV2()
Wraps up work for a task. Wrap up reason is applied after the task has been ended either by the agent or by the customer. A wrap up is essential and is the last step in an agent's flow of handling tasks.

**Example**

```javascript
await Desktop.agentContact.wrapupV2({
    interactionId: "dab1a2f0-bad0-11ea-8e7c-0d99ede2535a",
    data: {
        wrapUpReason: "Sales",
        auxCodeId: "AXUH3oN12eV-WekpnDpl",
        isAutoWrapup: false,
    }
});
```

**Payload type**

```typescript
type RequestPayload = {
    interactionId: string;data: Contact.WrapupPayLoad
};
```

The following table lists the payload details:

| Name            | Type    | Description                                                                                                                                | Required |
| --------------- | ------- | ------------------------------------------------------------------------------------------------------------------------------------------ | -------- |
| interactionId   | String  | Unique identifier for the user interaction.                                                                                                | Yes      |
| data            | Object  | Options of the wrap up.                                                                                                                    | Yes      |
| -->wrapUpReason | String  | Every wrap up reason will have an unique auxillary code. Use this field to specify the reason for wrapping up the call, maximum length 128 characters.                                                                        | Yes      |
| -->auxCodeId    | String  | Auxiliary codes are status codes which an agent can select in Webex Contact Center Agent Desktop. They are of two types: Idle and Wrap-Up codes, and every agent profile must have one of each for the agent to use.  Wrap-up codes indicate the result of customer contacts, such as successful resolution or escalation of the contact. Creating and managing auxiliary codes requires an administrator role and the appropriate cjp:config_write or cjp:config_read scopes, maximum length 36 characters.                                                                                                      | Yes      |
| -->isAutoWrapup | Boolean | Determines whether the auto wrap up is enabled or not.<br><br>- True—The auto warp up is enabled.<br>- False—The auto warp up is disabled. | Yes      |

**Returns**
`{Object}` The object with the retrieved data.

**Note:** The `type` parameter value in the response payload depends on the success or failure of the method. If the method is successful, the value is `AgentWrappedUp`; else, `AgentWrapupFailed`.

**Example Response**

```javascript
const wrapUpResponse = {
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
                "vteamId": "AXCqFyz1G2pKap9PI-mW"
            },
            "contactDirection": {
                "type": "INBOUND"
            },
            "currentVTeam": "3270",
            "interactionId": "a66d05ab-40ab-11eb-b59a-7d3326b3ffc1",
            "isFcManaged": false,
            "isTerminated": true,
            "media": {},
            "mediaChannel": "web",
            "mediaType": "chat",
            "orgId": "f111e3af-1a45-42ef-9erf-4562354b8a25",
            "outboundType": null,
            "owner": "7d12d9ea-e8e0-41ee-81bf-c11a685b64ed",
            "participants": {
                "janedoe@gmail.com": {
                    "id": "janedoe@gmail.com",
                    "pType": "Customer",
                    "type": "Customer"
                }
            },
            "previousVTeams": [],
            "state": "connected"
        },
        "interactionId": "a66d05ab-40ab-11eb-b59a-7d3326b3ffc1",
        "orgId": "f111e3af-1a45-42ef-9erf-4562354b8a25",
        "queueMgr": "aqm",
        "trackingId": "5272a610-40ac-11eb-8866-d7ef6ff89aa6",
        "type": "AgentWrappedUp",
        "wrapUpAuxCodeId": "0"
    },
    "orgId": "f111e3af-1a45-42ef-9erf-4562354b8a25",
    "trackingId": "notifs_b5e0ebb7-fd1d-479f-8663-81a64030cee6",
    "type": "RoutingMessage"
}
```

## Verify Interaction Changes

Subscribe to the relevant [contact events](https://developer.webex.com/docs/desktop-contact-events) and check both success and failure events. Register listeners while the widget is mounted and remove them when it disconnects.

## Related Pages

- [Agent Desktop overview](https://developer.webex.com/docs/desktop)
- [Desktop SDK Reference](https://developer.webex.com/docs/desktop-sdk-reference)
