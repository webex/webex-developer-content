---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-outbound-callbacks
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Dialer Module
- Methods
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/desktop-outbound-callbacks). [Full Markdown](../../../../docs/desktop-outbound-callbacks.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before You Begin](001-before-you-begin.md)

## Article introduction

Initiate outbound calls, update call-associated data, and manage scheduled callbacks with the Desktop SDK.

## Parent context

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

## Selected section

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
