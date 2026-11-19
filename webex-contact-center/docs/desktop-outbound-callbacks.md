---
type: Guide
title: Outbound Calls and Scheduled Callbacks
display_title: Outbound Calls and Scheduled Callbacks
canonical_url: https://developer.webex.com/docs/desktop-outbound-callbacks
content_type: documentation
product_group:
- webex-contact-center
categories:
- webex-contact-center
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/desktop-outbound-callbacks)

Initiate outbound calls, update call-associated data, and manage scheduled callbacks with the Desktop SDK.

## Before You Begin

Install and initialize the SDK as described in [Get Started with the Desktop SDK](https://developer.webex.com/docs/desktop-sdk-getting-started). Your widget must run inside Webex Contact Center Desktop.

## Address Books and Outbound ANI

These methods belong to `Desktop.agentStateInfo`.

### fetchAddressBooks()

Retrieves the address book details.

**Example**

```javascript
const books = await Desktop.agentStateInfo.fetchAddressBooks();
```

**Returns**
`{Object}` The address book response. Its `speedDials` property is an array of address entries.

**Example Response**

```javascript
const addressBooks = {
    speedDials: [{
            desc: 'Jane Doe',
            dn: '9997770094'
        },
        {
            desc: 'John Doe',
            dn: '9997770095'
        },
    ]
};
```

**Address type**

```typescript
type Address = {
    desc: string;
    dn: string;
    phoneBookName ? : string;
};
```

### mockOutdialAniList()

Fetches the ANI list that is used for an outdial call. The administrator adds the outdial ANI list to an agent profile. The outdial number is used as the caller number, and is displayed to the customer as the caller ID.
Updates the store variable value as per the response received from `mockOutdialAniList`. (Initially the store variable value will be empty).

**Store Variable**

```javascript
STORE.agent.outdialAniList
```

**Example**

```javascript
await Desktop.agentStateInfo.mockOutdialAniList();
```

**Returns**
`{Object}` Lists the outdial ANI.

**Example Response**

```javascript
const mockOutdialAniListResponse = {
  data: {
    agentSessionId: "",
    callData: "",
    data: {
      mockOutdialAniList: [
        {
          id: "+1-3364112001",
          name: "outdial ani"
        },
        {
          id: "+1-3364112002",
          name: "outdial ani two"
        },
        {
          id: "+1-3364112003",
          name: "outdial ani three"
        },
        {
          id: "+1-3364112004",
          name: "outdial ani four"
        }
      ]
    },
    jsMethod: "mockOutdialAni"
  },
  orgId: "b33fb142-4d65-4781-9899-19b0363cd45f",
  trackingId: "notifs_b3cf873d-56e4-4f6b-801d-c0dc49f3dd87",
  type: "mockOutdialAniList"
};
```

## Dialer Module

The `Desktop.dialer` module makes requests and listens to notification events related to the outdial activity (outgoing customer calls initiated by agents).

**Example**

```javascript
import {
    Desktop
} from "@wxcc-desktop/sdk";
// Other widget setup omitted.
const outdial = await Desktop.dialer.startOutdial({
    data: {
        entryPointId: "1212312567",
        destination: "12078995678",
        origin: "+1-3364112001",
        direction: "OUTBOUND",
        attributes: {},
        mediaType: "telephony",
        outboundType: "OUTDIAL"
    }
});

logger.info("Dialer outdial: ", outdial);

// List of available subscription events:
Desktop.dialer.addEventListener("eOutdialFailed", msg => logger.info(msg));
```

To remove an event subscription in order to avoid memory leaks, you have the following options:

```javascript
// Module supports removing added listeners like:
const listener = (msg) => logger.info(msg);
Desktop.dialer.addEventListener("eOutdialFailed", listener);
Desktop.dialer.removeEventListener("eOutdialFailed", listener);

// Module supports one-time added listeners like:
Desktop.dialer.addOnceEventListener("eOutdialFailed", listener);
Desktop.dialer.removeOnceEventListener("eOutdialFailed", listener);

// Module supports removing all listeners like:
Desktop.dialer.removeAllEventListeners();
```

### Methods

#### startOutdial(data)

Initiates an outdial call.

**Example**

```javascript
await Desktop.dialer.startOutdial({
    data: {
        entryPointId: "1212312567",
        destination: "12078995678",
        direction: "OUTBOUND",
    origin: "67078005678",
        attributes: {},
        mediaType: "telephony",
        outboundType: "CourtesyCallback"
    }
});
```

**Parameters**

| Name            | Type   | Description                                                        | Required |
| --------------- | ------ | ------------------------------------------------------------------ | -------- |
| data            | Object | Options for the outdial call.                                      | Yes      |
| -->entryPointId | String | Unique identifier of the outdial entry point.                      | Yes      |
| -->destination  | String | Dial number of the end recipient.                                  | Yes      |
| -->direction    | String | Direction of call from a dialer to recipient.                      | Yes      |
| -->origin       | String | To add any outdial ANI value.                                      | Yes      |
| -->attributes   | Object | Options of the attributes.                                         | Optional |
| -->mediaType    | String | The media channel type such as telephony, social, email, and chat. | Yes      |
| -->outboundType | String | Type of an outdial call such as OUTDIAL, CourtesyCallback.         | Yes      |

**Returns**
`{Object}` The object with the retrieved data.

**Example Response**

```javascript
const startOutdialResponse = {
  data: {
    agentId: "7c867aa9-ec768-341a-b767-e5hd6ae7g701",
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
        outdialTransferToQueueEnabled: "false",
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
      interactionId: "8da312bb-5349-4d97-89d9-7bedd01b8782",
      isFcManaged: false,
      isTerminated: false,
      media: {
        "8da312bb-5349-4d97-89d9-7bedd01b8782": {
          holdTimestamp: null,
          isHold: false,
          mType: "mainCall",
          mediaMgr: "vmm",
          mediaResourceId: "8da312bb-5349-4d97-89d9-7bedd01b8782",
          mediaType: "telephony",
          participants: []
        }
      },
      mediaChannel: "dialer",
      mediaType: "telephony",
      orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
      outboundType: "OUTDIAL",
      owner: "7c867aa9-ec768-341a-b767-e5hd6ae7g701",
      participants: {
        "7c867aa9-ec768-341a-b767-e5hd6ae7g701": {
          channelId: "0717a2ce-76cd-4ba4-9053-71f2c78168b8",
          consultState: null,
          consultTimestamp: null,
          dn: "8895579172",
          hasJoined: false,
          id: "7c867aa9-ec768-341a-b767-e5hd6ae7g701",
          isConsulted: false,
          isWrapUp: false,
          joinTimestamp: null,
          lastUpdated: 1612345959131,
          name: "Jane Doe",
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
      state: "new",
      workflowManager: null
    },
    interactionId: "8da312bb-5349-4d97-89d9-7bedd01b8782",
    mediaResourceId: "8da312bb-5349-4d97-89d9-7bedd01b8782",
    orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
    queueMgr: "aqm",
    ronaTimeout: 30,
    trackingId: "cfe421df-f107-42f3-945b-a6da5dd13ccd",
    type: "AgentOfferContact"
  },
  orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
  trackingId: "notifs_a6cfbcc4-7a8c-4a2e-a9d5-6c23683cdcb7",
  type: "RoutingMessage"
};
```

#### updateCadVariables()

Updates the Call-Associated Data (CAD) variables of a task.

**Example**

```javascript
try {
  await Desktop.dialer.updateCadVariables({
    interactionId: "842ba17b-9902-4420-8607-ea89a13ab332111",
    data: {
      attributes: {
        Global_FeedbackSurveyOptIn: "uninitialized"
      }
    }
  });
} catch (e) {
  // Handle Exception
}
```

**Note:** You can add a JavaScript try-catch block to pass the error code and handle the exceptions.

**Parameters**

| Name          | Type   | Description                                                                                                   | Required |
| ------------- | ------ | ------------------------------------------------------------------------------------------------------------- | -------- |
| interactionId | String | Unique identifier for the user interaction.                                                                   | Yes      |
| data          | Object | Options to update CAD variables.                                                                              | Yes      |
| -->attributes | Object | Options for the attributes.                                                                                   | Yes      |
| -->name       | String | Key (unique identifier) for the CAD variable. <br> **Note:** You can have a maximum of 30 CAD variables.</br> | Yes      |
| -->value      | String | Value of the CAD variable. <br> **Note:** You can have a maximum of 256 characters. </br>                     | Yes      |

**Returns**

`{Object}` The object with the retrieved data.

**Example Response**

```javascript
const updateCadVariablesResponse = {
  data: {
    agentId: null,
    eventType: "RoutingMessage",
    interaction: {
      callAssociatedData: {
        AgentID: {
          agentEditable: true,
          agentViewable: true,
          displayName: "AgentIId",
          global: false,
          name: "AgentID",
          reportable: false,
          type: "STRING",
          value: "Test"
        },
        Global_FeedbackSurveyOptIn: {
          agentEditable: true,
          agentViewable: true,
          displayName: "Post Call Survey Opt-in",
          global: false,
          name: "Global_FeedbackSurveyOptIn",
          reportable: false,
          type: "STRING",
          value: "uninitialized"
        },
        Global_Language: {
          agentEditable: false,
          agentViewable: true,
          displayName: "Customer Language",
          global: false,
          name: "Global_Language",
          reportable: false,
          type: "STRING",
          value: "en-US"
        },
        InteractionId: {
          agentEditable: true,
          agentViewable: true,
          displayName: "Interaction ID",
          global: false,
          name: "InteractionId",
          reportable: false,
          type: "STRING",
          value: "842ba17b-9902-4420-8607-ea89a13ab332111"
        },
        ani: {
          agentEditable: false,
          agentViewable: true,
          displayName: "ani",
          global: false,
          name: "ani",
          reportable: false,
          type: "STRING",
          value: "+12157702012"
        },
        dn: {
          agentEditable: false,
          agentViewable: true,
          displayName: "dn",
          global: false,
          name: "dn",
          reportable: false,
          type: "STRING",
          value: "+12147659005"
        },
        ronaTimeout: {
          agentEditable: false,
          agentViewable: true,
          displayName: "ronaTimeout",
          global: false,
          name: "ronaTimeout",
          reportable: false,
          type: "STRING",
          value: "18"
        },
        test: {
          agentEditable: false,
          agentViewable: true,
          displayName: "test",
          global: false,
          name: "test",
          reportable: false,
          type: "BOOLEAN",
          value: "true"
        },
        virtualTeamName: {
          agentEditable: false,
          agentViewable: true,
          displayName: "virtualTeamName",
          global: false,
          name: "virtualTeamName",
          reportable: false,
          type: "STRING",
          value: "Queue - Telephony"
        }
      },
      callAssociatedDetails: {
        InteractionId: "842ba17b-9902-4420-8607-ea89a13ab332111",
        ani: "+12157702012",
        dn: "+12147659005",
        ronaTimeout: "18",
        virtualTeamName: "Queue - Telephony"
      },
      callFlowParams: {},
      callProcessingDetails: {
        CONTINUE_RECORDING_ON_TRANSFER: "true",
        EP_ID: "AXUCQa9666OI4n5klmFgk",
        QMgrName: "aqm",
        QueueId: "AXCZ0riRefBr7nI0lIHo",
        ani: "+12167702012",
        dnis: "+12137659005",
        fceRegisteredEvents: "",
        isParked: "false",
        mohFileName: "defaultmusic_on_hold.wav",
        participantInviteTimeout: "false",
        pauseDuration: "10",
        pauseResumeEnabled: "true",
        priority: "10",
        recordInProgress: "true",
        recordingStarted: "true",
        ronaTimeout: "18",
        routingStrategyId: "AXUCRX6iQA-8GMFVNc5I",
        taskToBeSelfServiced: "false",
        tenantId: "133",
        virtualTeamName: "Queue - Telephony",
        vteamId: "AXCZ0riRe7Br7nI0lIHo",
        workflowId: "5fb7b590349a083b26f23322",
        workflowName: "basic-call-flow"
      },
      contactDirection: {
        type: "INBOUND"
      },
      currentVTeam: "AXCZ0riRefBr7nI0lIHo",
      interactionId: "842ba17b-9902-4420-8607-ea89a13ab332",
      isFcManaged: true,
      isTerminated: true,
      media: {
        "842ba17b-9902-4420-8607-ea89a13ab332": {
          holdTimestamp: null,
          isHold: false,
          mType: "mainCall",
          mediaMgr: "vmm",
          mediaResourceId: "842ba17b-9902-4420-8607-ea89a13ab332",
          mediaType: "telephony",
          participants: ["+12157702012", "f9dfc80e-bc9f-4793-8714-055a8e0ec715"]
        }
      },
      mediaChannel: "broadcloud",
      mediaType: "telephony",
      orgId: "f222e3af-1a53-42ef-9deb-7520034b8a10",
      outboundType: null,
      owner: "f9dfc80e-bc9f-4793-8714-055a8e0ec715",
      participants: {
        "+12157702012": {
          id: "+12157702012",
          pType: "Customer",
          type: "Customer"
        },
        "f9dfc80e-bc9f-4793-8714-055a8e0ec715": {
          channelId: "8a979027-9f74-4e14-b2c2-db8ea0261275",
          consultState: null,
          consultTimestamp: null,
          dn: "+19997770103",
          hasJoined: true,
          id: "f9dfc80e-bc9f-4793-8714-055a8e0ec715",
          isConsulted: false,
          isWrapUp: true,
          joinTimestamp: 1634646818059,
          lastUpdated: 1634646838590,
          name: "Archana R",
          pType: "Agent",
          queueId: "AXCZ0riRefBr7nI0lIHo",
          queueMgrId: "aqm",
          sessionId: "98ba1262-1f77-4d74-a8f8-d36d670983eb",
          siteId: "473",
          skillId: null,
          skillName: null,
          skills: [],
          teamId: "962",
          teamName: "Team X",
          type: "Agent",
          wrapUpTimestamp: 1634646838590
        }
      },
      previousVTeams: ["AXUCQa9W1OI4n5klmFgk"],
      queuedTimestamp: null,
      state: "connected",
      workflowManager: null
    },
    interactionId: "842ba17b-9902-4420-8607-ea89a13ab332",
    orgId: "f222e3af-1a53-42ef-9deb-7520034b8a10",
    queueMgr: "aqm",
    trackingId: "adb6b600-8d28-4c32-bf50-5b190baae07d",
    type: "ContactUpdated",
    updatedBy: "f9dfc80e-bc9f-4793-8714-055a8e0ec715"
  }
};
```

### Events

#### eOutdialFailed

Outdial call did not succeed.

**Example**

```javascript
Desktop.dialer.addEventListener("eOutdialFailed", (msg) => logger.info(msg));
```

**Example Response**

```javascript
const eOutdialFailed = {
  agentId: "7c867aa9-ec768-341a-b767-e5hd6ae7g701",
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
      outdialTransferToQueueEnabled: "false",
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
    interactionId: "d87dac90-4f81-486c-8deb-b94bbcd21e92",
    isFcManaged: false,
    isTerminated: true,
    media: {
      "d87dac90-4f81-486c-8deb-b94bbcd21e92": {
        holdTimestamp: null,
        isHold: false,
        mType: "mainCall",
        mediaMgr: "vmm",
        mediaResourceId: "d87dac90-4f81-486c-8deb-b94bbcd21e92",
        mediaType: "telephony",
        participants: []
      }
    },
    mediaChannel: "dialer",
    mediaType: "telephony",
    orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
    outboundType: "OUTDIAL",
    owner: "7c867aa9-ec768-341a-b767-e5hd6ae7g701",
    participants: {
      "7c867aa9-ec768-341a-b767-e5hd6ae7g701": {
        channelId: "0717a2ce-76cd-4ba4-9053-71f2c78168b8",
        consultState: null,
        consultTimestamp: null,
        dn: "8895579172",
        hasJoined: false,
        id: "7c867aa9-ec768-341a-b767-e5hd6ae7g701",
        isConsulted: false,
        isWrapUp: false,
        joinTimestamp: null,
        lastUpdated: 1612346591051,
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
    state: "new",
    workflowManager: null
  },
  interactionId: "d87dac90-4f81-486c-8deb-b94bbcd21e92",
  mediaType: "telephony",
  orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
  queueId: "3264",
  queueMgr: "aqm",
  reason: "CUSTOMER_UNAVAILABLE",
  reasonCode: 500,
  trackingId: "09f0d9fd-6cad-48a4-a906-be1b09a8fdc0",
  type: "AgentOutboundFailed"
};
```

## Schedule Callback Module

The `Desktop.scheduleCallback` module provides methods to manage scheduled callbacks, including fetching, creating, updating, and deleting scheduled callback entries for agents.

**Example**

The `Desktop.scheduleCallback` module provides `fetchByAssigneeAgentId`, `fetchByCallbackPhoneNumber`, `createScheduleCallback`, `updateCallBackDetails`, `deleteScheduleCallback`, and `getValidCampaignTimes`. The sections below show the required arguments for each method.

### Methods

#### fetchByAssigneeAgentId(data)

Fetches scheduled callbacks for a given assignee agent ID. Returns a paginated list of scheduled callbacks assigned to the specified agent.

**Example**

```javascript
const result = await Desktop.scheduleCallback.fetchByAssigneeAgentId({
  data: {
    page: 0,
    assigneeAgent: "7d12d9ea-e8e0-41ee-81bf-c11a685b64ed",
    sortBy: "scheduledTime",
    sortOrder: "desc"
  }
});
```

**Parameters**

| Name           | Type   | Description                                                                 | Required |
| -------------- | ------ | --------------------------------------------------------------------------- | -------- |
| data           | Object | Options for fetching scheduled callbacks.                                   | Yes      |
| -->page        | Number | Page number for pagination (0-indexed).                                     | Yes      |
| -->assigneeAgent | String | Unique identifier of the assignee agent.                                  | Yes      |
| -->sortBy      | String | Field to sort results by (e.g., "scheduledTime").                           | No       |
| -->sortOrder   | String | Sort order direction. Possible values: "asc", "desc".                       | No       |

**Returns**

`{Object}` The object containing a `data` array of scheduled callbacks and a `meta` object with pagination information.

**Example Response**

```javascript
const fetchByAssigneeAgentIdResponse = {
  data: [
    {
      id: "4a86a573-4c5c-41f5-8970-a562488030d7",
      callbackOrigin: "api",
      createdTimestamp: "2026-01-28T10:30:00.000Z",
      lastUpdatedTimestamp: "2026-01-28T10:30:00.000Z",
      customerName: "John Doe",
      callbackNumber: "1234567890",
      timezone: "Asia/Calcutta",
      scheduleDate: "2026-02-01",
      startTime: "10:00:00",
      endTime: "11:00:00",
      assigneeAgent: "7d12d9ea-e8e0-41ee-81bf-c11a685b64ed",
      queueId: "3cc44ceb-8287-4004-934d-ceaefeb170ad",
      callbackReason: "Follow-up call"
    }
    // ... more callbacks
  ],
  meta: {
    orgId: "12345678-abcd-efgh-ijkl-mnopqrstuvwx",
    page: 0,
    pageSize: 100,
    totalPages: 1,
    totalRecords: 1,
    links: {
      self: "/v1/callbacks/organization/.../scheduled-callback?..."
    }
  }
};
```

#### fetchByCallbackPhoneNumber(data)

Fetches scheduled callbacks for a given callback phone number. Returns a paginated list of scheduled callbacks matching the specified phone number.

**Example**

```javascript
const result = await Desktop.scheduleCallback.fetchByCallbackPhoneNumber({
  data: {
    page: 0,
    phoneNumber: "1234567890"
  }
});
```

**Parameters**

| Name           | Type   | Description                                                                 | Required |
| -------------- | ------ | --------------------------------------------------------------------------- | -------- |
| data           | Object | Options for fetching scheduled callbacks.                                   | Yes      |
| -->page        | Number | Page number for pagination (0-indexed).                                     | Yes      |
| -->phoneNumber | String | The callback phone number to search for.                                    | Yes      |

**Returns**

`{Object}` The object containing a `data` array of scheduled callbacks and a `meta` object with pagination information.
**Example Response**

```javascript
const fetchByCallbackPhoneNumberResponse = {
  data: [
    {
      id: "8c4e2f1a-3b5d-4e7f-9a1c-6d8e2f4a5b3c",
      callbackOrigin: "api",
      createdTimestamp: "2026-01-28T10:30:00.000Z",
      lastUpdatedTimestamp: "2026-01-28T10:30:00.000Z",
      customerName: "Jane Smith",
      callbackNumber: "1234567890",
      timezone: "America/New_York",
      scheduleDate: "2026-02-05",
      startTime: "14:00:00",
      endTime: "15:00:00",
      queueId: "c3d4e5f6-a7b8-4c9d-0e1f-2a3b4c5d6e7f",
      callbackReason: "Product inquiry"
    }
    // ... more callbacks
  ],
  meta: {
    orgId: "12345678-abcd-efgh-ijkl-mnopqrstuvwx",
    page: 0,
    pageSize: 100,
    totalPages: 1,
    totalRecords: 1,
    links: {
      self: "/v1/callbacks/organization/.../scheduled-callback?..."
    }
  }
};
```

#### createScheduleCallback(data)

Creates a new scheduled callback entry. This method allows agents to schedule callbacks for customers with specified time windows and optional agent assignment.

**Example**

```javascript
const result = await Desktop.scheduleCallback.createScheduleCallback({
  data: {
    callbackNumber: "1234567890",
    customerName: "Customer Name",
    timezone: "Asia/Calcutta",
    scheduleDate: "2026-01-01",
    startTime: "10:00:00",
    endTime: "11:00:00",
    assigneeAgent: "7d12d9ea-e8e0-41ee-81bf-c11a685b64ed",
    queueId: "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
    callbackReason: "Callback Reason"
  }
});
```

**Parameters**

| Name              | Type   | Description                                                                                      | Required |
| ----------------- | ------ | ------------------------------------------------------------------------------------------------ | -------- |
| data              | Object | Options for creating a scheduled callback.                                                       | Yes      |
| -->callbackNumber | String | The phone number to call back.                                                                   | Yes      |
| -->customerName   | String | Name of the customer for non-campaign callback.                                                   | No       |
| -->campaignId     | String | Unique identifier of the campaign; used for campaign callback.                                    | No       |
| -->timezone       | String | Timezone for the scheduled callback (e.g., "Asia/Calcutta", "America/New_York").                 | Yes      |
| -->scheduleDate   | String | Date for the scheduled callback in YYYY-MM-DD format.                                            | Yes      |
| -->startTime      | String | Start time of the callback window in HH:MM:SS format.                                            | Yes      |
| -->endTime        | String | End time of the callback window in HH:MM:SS format.                                              | Yes      |
| -->assigneeAgent  | String | Unique identifier of the agent to assign the callback.                                           | No       |
| -->queueId        | String | Unique identifier of the queue for the callback.                                                 | Yes      |
| -->callbackReason | String | Reason for the callback.                                                                         | Yes      |
| -->sourceInteraction | String | Source interaction id. This is the interaction id of the interaction that triggered the callback. | No       |

**Returns**

`{Object}` The created scheduled callback object.

**Example Response**

```javascript
const createScheduleCallbackResponse = {
  id: "c89cd57d-79f8-4fc7-b2ec-06aeb4684017",
  customerName: "Customer Name",
  callbackNumber: "1234567890",
  timezone: "Asia/Calcutta",
  scheduleDate: "2026-01-01",
  startTime: "10:00:00",
  endTime: "11:00:00",
  queueId: "2533784e-a89d-452e-baab-b5fb0c5fa0d7",
  callbackReason: "Callback Reason",
  sourceInteraction: null,
  callbackOrigin: "api",
  createdTimestamp: 1738231200000,
  lastUpdatedTimestamp: 1738231200000,
  assigneeAgent: "7d12d9ea-e8e0-41ee-81bf-c11a685b64ed",
  assignedTime: 1738231199000,
  orgId: "58f1a59e-245c-4536-9ee4-06560658e493",
  callbackType: "scheduled_personal"
};
```

#### updateCallBackDetails(data)

Updates an existing scheduled callback entry. All callback details can be modified except the callback ID.

**Example**

```javascript
const result = await Desktop.scheduleCallback.updateCallBackDetails({
  data: {
    id: "9f1e2d3c-4b5a-6c7d-8e9f-0a1b2c3d4e5f",
    callbackNumber: "1234567890",
    customerName: "Updated Customer Name",
    timezone: "Asia/Calcutta",
    scheduleDate: "2026-01-01",
    startTime: "10:00:00",
    endTime: "11:00:00",
    assigneeAgent: "7d12d9ea-e8e0-41ee-81bf-c11a685b64ed",
    queueId: "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
    callbackReason: "Updated Callback Reason"
  }
});
```

**Parameters**

| Name              | Type   | Description                                                                                      | Required |
| ----------------- | ------ | ------------------------------------------------------------------------------------------------ | -------- |
| data              | Object | Options for updating a scheduled callback.                                                       | Yes      |
| -->id             | String | Unique identifier of the scheduled callback to update.                                          | Yes      |
| -->callbackNumber | String | The phone number to call back.                                                                   | Yes      |
| -->customerName   | String | Name of the customer for non-campaign callback.                                                  | No       |
| -->campaignId     | String | Unique identifier of the campaign; used for campaign callback.                                   | No       |
| -->timezone       | String | Timezone for the scheduled callback (e.g., "Asia/Calcutta", "America/New_York").                 | Yes      |
| -->scheduleDate   | String | Date for the scheduled callback in YYYY-MM-DD format.                                            | Yes      |
| -->startTime      | String | Start time of the callback window in HH:MM:SS format.                                            | Yes      |
| -->endTime        | String | End time of the callback window in HH:MM:SS format.                                              | Yes      |
| -->assigneeAgent  | String | Unique identifier of the agent to assign the callback.                                           | No       |
| -->queueId        | String | Unique identifier of the queue for the callback.                                                 | Yes      |
| -->callbackReason | String | Reason for the callback.                                                                         | Yes      |

**Returns**

`{Object}` The updated scheduled callback object.

**Example Response**

```javascript
const updateCallBackDetailsResponse = {
  id: "c89cd57d-79f8-4fc7-b2ec-06aeb4684017",
  customerName: "Updated Customer Name",
  callbackNumber: "1234567890",
  timezone: "Asia/Calcutta",
  scheduleDate: "2026-01-01",
  startTime: "10:00:00",
  endTime: "11:00:00",
  queueId: "2533784e-a89d-452e-baab-b5fb0c5fa0d7",
  callbackReason: "Updated Callback Reason",
  sourceInteraction: null,
  callbackOrigin: "api",
  createdTimestamp: 1738231200000,
  lastUpdatedTimestamp: 1738234800000,
  assigneeAgent: "7d12d9ea-e8e0-41ee-81bf-c11a685b64ed",
  assignedTime: 1738231199000,
  orgId: "58f1a59e-245c-4536-9ee4-06560658e493",
  callbackType: "scheduled_personal"
};
```

#### deleteScheduleCallback(data)

Deletes a scheduled callback entry by its unique identifier.

**Example**

```javascript
const result = await Desktop.scheduleCallback.deleteScheduleCallback({
  data: {
    id: "9f1e2d3c-4b5a-6c7d-8e9f-0a1b2c3d4e5f"
  }
});
```

**Parameters**

| Name   | Type   | Description                                                              | Required |
| ------ | ------ | ------------------------------------------------------------------------ | -------- |
| data   | Object | Options for deleting a scheduled callback.                               | Yes      |
| -->id  | String | Unique identifier (UUID) of the scheduled callback to delete.            | Yes      |

**Note:** The `id` parameter must be a valid UUID format.

#### getValidCampaignTimes(data)

Retrieves valid campaign callback time slots for a given campaign and agent. Use this method to get the campaign's weekly schedule and date overrides so that agents can schedule callbacks only within allowed time windows (for example, when creating a scheduled callback from a campaign interaction).

**Example**

```javascript
const result = await Desktop.scheduleCallback.getValidCampaignTimes({
  data: {
    campaignId: "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
    agentId: "7d12d9ea-e8e0-41ee-81bf-c11a685b64ed",
    interactionId: "f1e2d3c4-b5a6-4c7d-8e9f-0a1b2c3d4e5f"
  }
});
```

**Parameters**

| Name            | Type   | Description                                                                 | Required |
| --------------- | ------ | --------------------------------------------------------------------------- | -------- |
| data            | Object | Options for fetching valid campaign times.                                  | Yes      |
| -->campaignId   | String | Unique identifier of the campaign.                                          | Yes      |
| -->agentId      | String | Unique identifier of the agent.                                             | Yes      |
| -->interactionId | String | Unique identifier of the interaction that triggered the callback (e.g. the campaign call). Optional. | No       |

**Returns**

`{Object}` The object containing `data` with the campaign's valid time configuration: time zone, weekly schedule (per day), date overrides, and a success flag.

**Example Response**

```javascript
const getValidCampaignTimesResponse = {
  type: "CampaignValidTimesResponse",
  orgId: "58f1a59e-245c-4536-9ee4-06560658e493",
  trackingId: "tracking-id-123",
  data: {
    type: "CampaignValidTimesResponse",
    agentId: "7d12d9ea-e8e0-41ee-81bf-c11a685b64ed",
    campaignId: "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
    result: true,
    timeZone: "America/New_York",
    eventType: "CampaignValidTimesResponse",
    eventTime: 1738231200000,
    orgId: "58f1a59e-245c-4536-9ee4-06560658e493",
    trackingId: "tracking-id-123",
    weeklySchedule: {
      monday: [{ start: "09:00", end: "13:00" }, { start: "14:00", end: "18:00" }],
      tuesday: [{ start: "09:00", end: "17:00" }],
      wednesday: [{ start: "10:00", end: "14:00" }],
      thursday: [{ start: "09:00", end: "13:00" }, { start: "14:00", end: "18:00" }],
      friday: [{ start: "09:00", end: "12:00" }],
      saturday: [{ start: "10:00", end: "15:00" }],
      sunday: []
    },
    dateOverrides: [
      {
        date: "2026-01-15",
        shiftTimes: [{ start: "11:00", end: "16:00" }]
      }
    ]
  }
};
```

The `data.weeklySchedule` object has keys for each day of the week (`monday` through `sunday`). Each day's value is an array of time slots with `start` and `end` in `"HH:mm"` format. The `data.dateOverrides` array lists specific dates (YYYY-MM-DD) with custom shift times that override the weekly schedule. Use `data.result` to confirm the request succeeded; use `data.timeZone` when displaying or validating schedule times.

## Related Pages

- [Agent Desktop overview](https://developer.webex.com/docs/desktop)
- [Desktop SDK Reference](https://developer.webex.com/docs/desktop-sdk-reference)
