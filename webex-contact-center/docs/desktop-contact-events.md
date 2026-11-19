---
type: Guide
title: Contact Events and Subscriptions
display_title: Contact Events and Subscriptions
canonical_url: https://developer.webex.com/docs/desktop-contact-events
content_type: documentation
product_group:
- webex-contact-center
categories:
- webex-contact-center
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/desktop-contact-events)

Subscribe to Desktop contact events and use their payloads to keep widgets synchronized with interactions.

## Before You Begin

Install and initialize the SDK as described in [Get Started with the Desktop SDK](https://developer.webex.com/docs/desktop-sdk-getting-started). Your widget must run inside Webex Contact Center Desktop.

## Agent Contact Module

The `Desktop.agentContact` module makes requests and listens to notification events related to the agent-contact entity, such as the arrival of a new task.

**Example**

The [Desktop SDK Reference](https://developer.webex.com/docs/desktop-sdk-reference#methods-and-properties) lists the contact methods and links to their request payloads. Subscribe to the events your widget needs, and keep the handler reference so you can remove it when the widget disconnects.

```javascript
const onAssigned = message => console.log(message);
Desktop.agentContact.addEventListener("eAgentContactAssigned", onAssigned);

// When the widget disconnects:
function cleanupAssignedListener() {
  Desktop.agentContact.removeEventListener("eAgentContactAssigned", onAssigned);
}
```

**Example Response**

```typescript
// Common fields in contact-event data. Fields vary by event and may be absent.
type AgentContactEventData = {
    mediaResourceId?: string;
    eventType?: string;
    agentId?: string;
    destAgentId?: string | null;
    trackingId?: string;
    consultMediaResourceId?: string | null;
    interaction?: {
        isFcManaged?: boolean;
        isTerminated?: boolean;
        mediaType?: "email" | "chat" | "telephony" | "social" | "sms" | "facebook" | string;
        previousVTeams?: string[];
        state?: string;
        currentVTeam?: string;
        participants?: Record<string, unknown>;
        interactionId?: string;
        orgId?: string;
        owner?: string;
    },
    interactionId?: string;
    orgId?: string;
    owner?: string;
    queueMgr?: string;
    type?: string;
    ronaTimeout?: number;
    isConsulted?: boolean;
    isConferencing?: boolean;
    updatedBy?: string;
    destinationType?: string;
}
```

## Asynchronous Events

In order to subscribe to asynchronous events, use the following events:

- eAgentContact

* eAgentContactAssigned
* eAgentContactAssignFailed
* eAgentContactEnded
* eAgentContactWrappedUp
* eAgentContactAniUpdated
* eAgentOfferContact
* eAgentOfferContactRona
* eAgentOfferConsult
* eAgentWrapup
* eAgentContactHeld
* eAgentContactUnHeld
* eCallRecordingStarted
* eResumeRecording
* ePauseRecording
* eConsultTransfer
* eAgentblindTransferred
* eAgentvteamTransfer
* eAgentConsultCreated
* eAgentConsultConferenced
* eAgentConsultEnded
* eAgentCtqCancelled
* eAgentConsultConferenceEnded
* eAgentConsulting
* eAgentConsultFailed
* eAgentConsultEndFailed
* eAgentCtqFailed
* eAgentCtqCancelFailed
* eAgentConsultConferenceEndFailed
* eAgentMonitorStateChanged
* eAgentMonitoringEnded
* eAgentOfferCampaignReserved
* eAgentAddCampaignReserved
* eParticipantLeftConference
* eAgentConsultTransferring
* eAgentConsultConferencing
* eParticipantJoinedConference
* eContactOwnerChanged
* eAgentCampaignContactUpdated

**Example**

```javascript
const onAssigned = (message) => console.log("Contact assigned:", message);
Desktop.agentContact.addEventListener("eAgentContactAssigned", onAssigned);

// During widget teardown:
function cleanupAssignedListener() {
  Desktop.agentContact.removeEventListener("eAgentContactAssigned", onAssigned);
}
```

To remove an event subscription in order to avoid memory leaks, use the following options:

```javascript
// Module supports removing added listeners like:
const listener = (msg) => console.log(msg);
Desktop.agentContact.addEventListener("eAgentContact", listener);
Desktop.agentContact.removeEventListener("eAgentContact", listener);

// Module supports one-time added listeners like:
Desktop.agentContact.addOnceEventListener("eAgentContact", listener);
Desktop.agentContact.removeOnceEventListener("eAgentContact", listener);

// Module supports removing all listeners like:
Desktop.agentContact.removeAllEventListeners();
```

**Note:** It is recommended to rely on the events, than on the responses of the asynchronous events such as stateChange.

Desktop custom widgets will receive events only when they are mounted. For a widget to be mounted always, you can consider persistent widgets or headless widgets. When you switch between pages, the widgets are unmounted from the previous page, and the changes made to widgets are lost. For more information, see the [Custom Widgets](https://help.webex.com/en-us/article/ng08gqeb/Create-custom-desktop-layout) section and [Create custom desktop layout](https://help.webex.com/en-us/article/ng08gqeb/Create-custom-desktop-layout) in Webex Help Center.

### Listener Methods

#### addEventListener(event, handler)

Adds an event listener. This method listens to a particular event if generated. The event name can be specified as a string to the parameter.

**Example**

```javascript
Desktop.agentContact.addEventListener("eAgentContact", msg => console.log(msg));
```

**Parameters**

| Name    | Type     | Description                                               | Required |
| ------- | -------- | --------------------------------------------------------- | -------- |
| event   | String   | Type of an event.                                         | Yes      |
| handler | Function | The function that is invoked when the conditions are met. | Yes      |

#### removeEventListener(event, handler)

Removes an added event listener that has been attached with the `addEventListener()` method.

**Example**

```javascript
const handler = (msg) => console.log(msg);
Desktop.agentContact.addEventListener("eAgentContact", handler);

// During widget cleanup, remove the same function reference.
function cleanupListener() {
  Desktop.agentContact.removeEventListener("eAgentContact", handler);
}
```

**Parameters**

| Name    | Type     | Description                                               | Required |
| ------- | -------- | --------------------------------------------------------- | -------- |
| event   | String   | Type of an event.                                         | Yes      |
| handler | Function | The function that is invoked when the conditions are met. | Yes      |

#### addOnceEventListener(event, handler)

Adds a one-time event listener.

**Example**

```javascript
Desktop.agentContact.addOnceEventListener(
  "eAgentContact",
  (msg) => console.log(msg)
);
```

**Parameters**

| Name    | Type     | Description                                               | Required |
| ------- | -------- | --------------------------------------------------------- | -------- |
| event   | String   | Type of an event.                                         | Yes      |
| handler | Function | The function that is invoked when the conditions are met. | Yes      |

#### removeOnceEventListener(event, handler)

Removes a one-time added event listener.

**Example**

```javascript
const handler = (msg) => console.log(msg);
Desktop.agentContact.addOnceEventListener("eAgentContact", handler);

// During widget cleanup, remove the same function reference.
function cleanupListener() {
  Desktop.agentContact.removeOnceEventListener("eAgentContact", handler);
}
```

**Parameters**

| Name    | Type     | Description                                               | Required |
| ------- | -------- | --------------------------------------------------------- | -------- |
| event   | String   | Type of an event.                                         | Yes      |
| handler | Function | The function that is invoked when the conditions are met. | Yes      |

#### removeAllEventListeners()

Removes all added event listeners.

**Example**

```javascript
Desktop.agentContact.removeAllEventListeners();
```

### Contact Event Catalog

#### eAgentContact

Loads the desktop with the agent tasks.

**Example**

```javascript
Desktop.agentContact.addEventListener(
  "eAgentContact",
  (msg) => console.log(msg)
);
```

**Example Response**

```javascript
const eAgentContact = {
  type: "RoutingMessage",
  orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
  trackingId: "notifs_6f0ee13d-bb2f-4600-8631-c7d86fb08dfe",
  data: {
    mediaResourceId: "80c213d5-2747-4bf4-8a0c-9c45b0afdf2a",
    eventType: "RoutingMessage",
    agentId: "9738292f-3a68-4909-bdea-b541cccd6935",
    trackingId: "68bca42c-8a50-4cf1-8c18-f5229b04afa9",
    interaction: {
      isFcManaged: false,
      isTerminated: false,
      mediaType: "telephony",
      previousVTeams: ["AXCZ0YCAXrf9I0XFBI7b"],
      state: "new",
      currentVTeam: "3268",
      participants: {
        "+19997770095": {
          id: "+19997770095",
          pType: "Customer",
          type: "Customer"
        },
        "9738292f-3a68-4909-bdea-b541cccd6935": {
          joinTimestamp: null,
          name: "",
          pType: "Agent",
          teamName: "Email_Team",
          lastUpdated: 1593440068730,
          teamId: "960",
          isConsulted: false,
          hasJoined: false,
          dn: "9997770093",
          queueId: "3268",
          id: "9738292f-3a68-4909-bdea-b541cccd6935",
          sessionId: "054ebc22-b34e-4e1b-8730-da294093f813",
          queueMgrId: "aqm",
          siteId: "472",
          type: "Agent",
          channelId: "53e05ff1-69c7-425f-a660-5f9e21f0a4bb",
          isWrapUp: false
        }
      },
      interactionId: "80c213d5-2747-4bf4-8a0c-9c45b0afdf2a",
      orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
      callProcessingDetails: {
        QMgrName: "aqm",
        taskToBeSelfServiced: "false",
        ani: "+19997770095",
        dnis: "+12147659000",
        tenantId: "133",
        QueueId: "3268",
        vteamId: "3268",
        jscriptId: "AXCZ4c3mjkwgAuS7vSIU",
        virtualTeamName: "Queue - Telephony",
        customerName: "Jane Doe",
        ronaTimeout: "30",
        reasonCode: "Credit",
        IvrPath: " EOI",
        pathId: " StartCall PlayDone out out out"
      },
      media: {
        "80c213d5-2747-4bf4-8a0c-9c45b0afdf2a": {
          mediaResourceId: "80c213d5-2747-4bf4-8a0c-9c45b0afdf2a",
          mediaType: "telephony",
          mediaMgr: "vmm",
          participants: ["+19997770095"],
          mType: "mainCall",
          isHold: false
        }
      },
      owner: "9738292f-3a68-4909-bdea-b541cccd6935",
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
          value: "Welcome to Contact Center"
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
    interactionId: "80c213d5-2747-4bf4-8a0c-9c45b0afdf2a",
    orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
    queueMgr: "aqm",
    type: "AgentContact",
    isConsulted: false,
    consultMediaResourceId: null
  }
};
```

#### eAgentContactAssigned

New task or contact has been assigned successfully.

**Example**

```javascript
Desktop.agentContact.addEventListener(
  "eAgentContactAssigned",
  (msg) => console.log(msg)
);
```

For more information on example response, see [accept](https://developer.webex.com/docs/desktop-call-control#accept).

#### eAgentContactAssignFailed

Assigned task or contact did not succeed.

**Example**

```javascript
Desktop.agentContact.addEventListener(
  "eAgentContactAssignFailed",
  (msg) => console.log(msg)
);
```

For more information on example response, see [accept](https://developer.webex.com/docs/desktop-call-control#accept).

#### eAgentContactWrappedUp

Accepted task or contact has been wrapped up.

**Example**

```javascript
Desktop.agentContact.addEventListener(
  "eAgentContactWrappedUp",
  (msg) => console.log(msg)
);
```

For more information on example response, see [wrapup](https://developer.webex.com/docs/desktop-call-control#wrapup).

#### eAgentContactAniUpdated

Task or contact ANI has been updated.

**Example**

```javascript
Desktop.agentContact.addEventListener(
  "eAgentContactAniUpdated",
  (msg) => console.log(msg)
);
```

**Example Response**

```javascript
const eAgentContactAniUpdated = {
  data: {
    eventType: "RoutingMessage",
    interactionId: "bd2b36fc-deec-44a4-8d37-ea175332b4f9",
    orgId: "8ee9d5a5-7099-43da-a468-4115a6849a8f",
    interaction: {
      interactionId: "80cf49a5-2449-4246-a891-76256b772e32",
      orgId: "6e30f3a2-500b-49c9-a091-fc9442a23466",
      state: "connected",
      mediaType: "telephony",
      ani: "888****066",
      callAssociatedDetails: {
        ani: "888****066",
        dnis: "+15*****8006",
        virtualTeamName: "webrtc_inbound_desktop"
      },
      callAssociatedData: {
        ani: {
          name: "ani",
          agentEditable: false,
          value: "888****066",
          type: "STRING",
          displayName: "ani",
          agentViewable: true,
          isSecure: false
        }
      },
      callProcessingDetails: {
        ani: "888****066",
        workflowName: "webrtc_inbound",
        queueId: "c0dcca57-55dd-466e-8c70-bd08b096f5a7",
        priority: "10",
        dnis: "+15*****8006"
      }
    },
    ani: "888****066",
    trackingId: "bbceaa12-6ab0-4e71-af16-7c612a6ef120",
    eventTime: 1742826471297,
    type: "ContactAniUpdated"
  }
};
```

#### eAgentOfferContact

New task or contact has been routed to an agent.

**Example**

```javascript
Desktop.agentContact.addEventListener(
  "eAgentOfferContact",
  (msg) => console.log(msg)
);
```

**Example Response**

```javascript
const eAgentOfferContact = {
  data: {
    agentId: "7d12d9ea-e8e0-41ee-81bf-c11a685b64ed",
    eventType: "RoutingMessage",
    interaction: {
      callAssociatedData: {
        ani: {
          value: "janedoe@gmail.com"
        },
        category: {
          value: "Automation"
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
          value: "Automation"
        },
        ronaTimeout: {
          value: "30"
        },
        roomTitle: {
          value: "Help Jane Doe with Automation"
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
        category: "Automation",
        customerName: "Jane Doe",
        dn: "Desktop",
        entryPointId: "AXCqFyz1G2pKap9PI-mW",
        guestId:
          "Y2lzY29zcGFyazovL3VzL1BFT1BMRS83ZjA3YjJmMC1jNTMyLTQ5MDktYTkzNi0yYTA3MTVmZGIwMTA",
        mediaChannel: "web",
        reason: "Test",
        reasonCode: "Automation",
        ronaTimeout: "30",
        roomTitle: "Help Jane Doe with Automation",
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
        category: "Automation",
        customerName: "Jane Doe",
        dnis: "Desktop",
        entryPointId: "AXCqFyz1G2pKap9PI-mW",
        guestId:
          "Y2lzY29zcGFyazovL3VzL1BFT1BMRS83ZjA3YjJmMC1jNTMyLTQ5MDktYTkzNi0yYTA3MTVmZGIwMTA",
        mediaChannel: "web",
        reason: "Test",
        reasonCode: "Automation",
        ronaTimeout: "30",
        roomTitle: "Help Jane Doe with Automation",
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
      interactionId: "8d3a56fa-4172-11eb-abaf-1b20df734401",
      isFcManaged: false,
      isTerminated: false,
      media: {
        Y2lzY29zcGFyazovL3VzL1JPT00vOTAxMmEzZjAtNDE3Mi0xMWViLWE1N2QtZWY2N2MwZTMyYmFh:
          {
            holdTimestamp: null,
            isHold: false,
            mType: "mainCall",
            mediaMgr: "cmm",
            mediaResourceId:
              "Y2lzY29zcGFyazovL3VzL1JPT00vOTAxMmEzZjAtNDE3Mi0xMWViLWE1N2QtZWY2N2MwZTMyYmFh",
            mediaType: "chat",
            participants: ["janedoe@gmail.com"]
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
          hasJoined: false,
          id: "7d12d9ea-e8e0-41ee-81bf-c11a685b64ed",
          isConsulted: false,
          isWrapUp: false,
          joinTimestamp: null,
          lastUpdated: 1608324587206,
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
      state: "new"
    },
    interactionId: "8d3a56fa-4172-11eb-abaf-1b20df734401",
    mediaResourceId:
      "Y2lzY29zcGFyazovL3VzL1JPT00vOTAxMmEzZjAtNDE3Mi0xMWViLWE1N2QtZWY2N2MwZTMyYmFh",
    orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
    queueMgr: "aqm",
    ronaTimeout: 30,
    trackingId: "429bb73d-7463-4661-94aa-a3230d60e88a",
    type: "AgentOfferContact"
  },
  orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
  trackingId: "notifs_f23e73e4-b130-4bce-b110-1c1da7225ffa",
  type: "RoutingMessage"
};
```

#### eAgentOfferContactRona

Agent failed to accept the task or contact request within the maximum available time. The system changes the agent state from Available to RONA.

**Example**

```javascript
Desktop.agentContact.addEventListener(
  "eAgentOfferContactRona",
  (msg) => console.log(msg)
);
```

For more information on example response, see [decline](https://developer.webex.com/docs/desktop-consultation-conferences#decline).

#### eAgentOfferConsult

Accepted task or contact consult request has been routed to an agent.

**Example**

```javascript
Desktop.agentContact.addEventListener(
  "eAgentOfferConsult",
  (msg) => console.log(msg)
);
```

**Example Response**

```javascript
export const eAgentOfferConsult = {
  type: "RoutingMessage",
  orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
  trackingId: "notifs_50e9d868-71c0-48f2-9880-4a12fc505988",
  data: {
    consultMediaResourceId:
      "consult_Y2lzY29zcGFyazovL3VzL1JPT00vODZkMGQ2MDAtOTQ0Yy0xMWVhLWE4MjMtNzFjMjA3YWRlYjAx",
    eventType: "RoutingMessage",
    agentId: "8546f083-74ae-4510-b2a6-c8e21f01689b",
    consultingAgentId: "9738292f-3a68-4909-bdea-b541cccd6935",
    trackingId: "ca074768-9d2b-427e-86af-3745c2a8cc60",
    interaction: {
      isFcManaged: false,
      isTerminated: false,
      mediaType: "chat",
      previousVTeams: [],
      state: "consult",
      currentVTeam: "3270",
      participants: {
        "mohaksin@cisco.com": {
          id: "mohaksin@cisco.com",
          pType: "Customer",
          type: "Customer"
        },
        "8546f083-74ae-4510-b2a6-c8e21f01689b": {
          name: "",
          pType: "Agent",
          teamName: "Dont_Use_Team",
          joinTimestamp: null,
          lastUpdated: 1589287209385,
          teamId: "964",
          isConsulted: true,
          hasJoined: false,
          dn: "9997770111",
          queueId: "3270",
          id: "8546f083-74ae-4510-b2a6-c8e21f01689b",
          sessionId: "dead6d11-3d8f-42ea-87d9-b94d5f5b6370",
          queueMgrId: "aqm",
          siteId: "472",
          type: "Agent",
          channelId: "a4297667-6d16-4d9d-ad2f-b21fee6b97fe",
          isWrapUp: false
        },
        "9738292f-3a68-4909-bdea-b541cccd6935": {
          name: "vivek",
          pType: "Agent",
          teamName: "Dont_Use_Team",
          joinTimestamp: 1594295035415,
          lastUpdated: 1589287209385,
          teamId: "964",
          isConsulted: false,
          hasJoined: true,
          dn: "9997770111",
          queueId: "3270",
          id: "9738292f-3a68-4909-bdea-b541cccd6935",
          sessionId: "dead6d11-3d8f-42ea-87d9-b94d5f5b6370",
          queueMgrId: "aqm",
          siteId: "472",
          type: "Agent",
          channelId: "a4297667-6d16-4d9d-ad2f-b21fee6b97fe",
          isWrapUp: false
        }
      },
      interactionId: "cd4f3721-944b-11ea-a5e5-bdac2bb8b026",
      orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
      callProcessingDetails: {
        QMgrName: "aqm",
        taskToBeSelfServiced: "false",
        ani: "mohaksin@cisco.com",
        dnis: "AgentX",
        tenantId: "133",
        QueueId: "3270",
        vteamId: "AXCqFyz1G2pKap9PI-mW",
        virtualTeamName: "Chat_Queue",
        customerName: "Mohak",
        ronaTimeout: "30",
        reasonCode: "Sales",
        reason: "Lockdown challeeeya",
        category: "Sales"
      },
      media: {
        Y2lzY29zcGFyazovL3VzL1JPT00vODZkMGQ2MDAtOTQ0Yy0xMWVhLWE4MjMtNzFjMjA3YWRlYjAx:
          {
            mediaResourceId:
              "Y2lzY29zcGFyazovL3VzL1JPT00vODZkMGQ2MDAtOTQ0Yy0xMWVhLWE4MjMtNzFjMjA3YWRlYjAx",
            mediaType: "chat",
            mediaMgr: "cmm",
            participants: ["mohaksin@cisco.com"],
            mType: "mainCall",
            isHold: false
          }
      },
      owner: "8546f083-74ae-4510-b2a6-c8e21f01689b",
      mediaChannel: "web",
      contactDirection: {
        type: "INBOUND"
      },
      callFlowParams: {
        Sales: {
          name: "Sales",
          qualifier: "vteam",
          description: "(vteam, A valid VTeam.)",
          valueDataType: "string",
          value: "3270"
        },
        Debit: {
          name: "Debit",
          qualifier: "vteam",
          description: "(vteam, A valid VTeam.)",
          valueDataType: "string",
          value: "3270"
        },
        Automation: {
          name: "Automation",
          qualifier: "vteam",
          description: "(vteam, A valid VTeam.)",
          valueDataType: "string",
          value: "3270"
        }
      }
    },
    ronaTimeout: 30,
    interactionId: "cd4f3721-944b-11ea-a5e5-bdac2bb8b026",
    orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
    queueMgr: "aqm",
    type: "AgentOfferConsult"
  }
};
```

#### eAgentWrapup

Accepted task or contact has been moved to a wrap up state.

**Example**

```javascript
Desktop.agentContact.addEventListener(
  "eAgentWrapup",
  (msg) => console.log(msg)
);
```

For more information on example response, see [end](https://developer.webex.com/docs/desktop-call-control#end).

#### eAgentContactHeld

Accepted task or contact has been put on hold.

**Example**

```javascript
Desktop.agentContact.addEventListener(
  "eAgentContactHeld",
  (msg) => console.log(msg)
);
```

For more information on example response, see [hold](https://developer.webex.com/docs/desktop-call-control#hold).

#### eAgentContactUnHeld

Accepted task or contact has been resumed.

**Example**

```javascript
Desktop.agentContact.addEventListener(
  "eAgentContactUnHeld",
  (msg) => console.log(msg)
);
```

For more information on example response, see [unHold()](https://developer.webex.com/docs/desktop-call-control#unhold).

#### eCallRecordingStarted

Call recording for an accepted task or contact has started.

**Example**

```javascript
Desktop.agentContact.addEventListener(
  "eCallRecordingStarted",
  (msg) => console.log(msg)
);
```

**Example Response**

```javascript
const eCallRecordingStarted = {
  data: {
    eventType: "RoutingMessage",
    interaction: {
      callAssociatedData: {
        ani: {
          agentEditable: false,
          displayName: "ani",
          name: "ani",
          type: "STRING",
          value: "9997652131"
        },
        dn: {
          agentEditable: false,
          displayName: "dn",
          name: "dn",
          type: "STRING",
          value: "9997651073"
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
          value: "qaus1-gt-requeue"
        }
      },
      callAssociatedDetails: {
        ani: "**********",
        dn: "**********",
        ronaTimeout: "30",
        virtualTeamName: "qaus1-gt-requeue"
      },
      callFlowParams: {
        OutdialQueue: {
          description: "(vteam, The Outdial Queue.)",
          name: "OutdialQueue",
          qualifier: "vteam",
          value: "4125",
          valueDataType: "string"
        }
      },
      callProcessingDetails: {
        QMgrName: "aqm",
        QueueId: "4125",
        agent_ani: "9997652131",
        ani: "**********",
        dnis: "**********",
        doNotRouteToAgents: "9b036d89-930c-4187-a5bd-5dbb1439fe41",
        outdialParkEpId: "AXRnbLmz1OI4n5klYr5E",
        outdialTransferToQueueEnabled: "true",
        pauseDuration: "30",
        pauseResumeEnabled: "true",
        recordInProgress: "true",
        ronaTimeout: "30",
        taskToBeSelfServiced: "false",
        tenantId: "82",
        virtualTeamName: "qaus1-gt-requeue",
        vteamId: "6838",
        vteamType: "inboundqueue"
      },
      contactDirection: {
        type: "OUTBOUND"
      },
      currentVTeam: "6838",
      interactionId: "28a8f08f-0d2f-46f9-9751-a2d9536886c1",
      isFcManaged: false,
      isTerminated: false,
      media: {
        "28a8f08f-0d2f-46f9-9751-a2d9536886c1": {
          holdTimestamp: null,
          isHold: false,
          mType: "mainCall",
          mediaMgr: "vmm",
          mediaResourceId: "28a8f08f-0d2f-46f9-9751-a2d9536886c1",
          mediaType: "telephony",
          participants: ["**********", "**********"]
        }
      },
      mediaChannel: "dialer",
      mediaType: "telephony",
      orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
      outboundType: "OUTDIAL",
      owner: "5b24107f-aae2-45e6-9bf8-a36d18b6f0e5",
      participants: {
        "5b24107f-aae2-45e6-9bf8-a36d18b6f0e5": {
          channelId: "1b61e3f4-9c33-4241-9304-9ea054b88be0",
          consultState: null,
          consultTimestamp: null,
          dn: "**********",
          hasJoined: true,
          id: "5b24107f-aae2-45e6-9bf8-a36d18b6f0e5",
          isConsulted: false,
          isWrapUp: false,
          joinTimestamp: 1612429637332,
          lastUpdated: 1612429637332,
          name: "qaus1-gt-requeue-user qaus1-gt-requeue-user",
          pType: "Agent",
          queueId: "6838",
          queueMgrId: "aqm",
          sessionId: "56d94e8d-fbd0-4933-936d-7c19f422ec47",
          siteId: "205",
          teamId: "1837",
          teamName: "integ-test-team",
          type: "Agent",
          wrapUpTimestamp: null
        },
        "**********": {
          id: "9997652131",
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
          isConsulted: false,
          isWrapUp: true,
          joinTimestamp: 1612429625705,
          lastUpdated: 1612429636839,
          name: "qaus1-gt-user1 qaus1-gt-user1",
          pType: "Agent",
          queueId: "4125",
          queueMgrId: "aqm",
          sessionId: "90896c91-0f77-4bc6-aec3-488a34ca88d3",
          siteId: "205",
          teamId: "598",
          teamName: "integ-test-team",
          type: "Agent",
          wrapUpTimestamp: 1612429636839
        }
      },
      previousVTeams: ["4125"],
      state: "connected",
      workflowManager: null
    },
    interactionId: "28a8f08f-0d2f-46f9-9751-a2d9536886c1",
    orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
    queueMgr: "aqm",
    trackingId: "795e3411-191d-4524-b01c-bf672126fe02",
    type: "ContactRecordingStarted"
  },
  orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
  trackingId: "notifs_9e18c618-cdd6-4bf7-be18-cafd250faabc",
  type: "RoutingMessage"
};
```

#### eResumeRecording

Resumes a voice call recording for an accepted task or contact.

**Example**

```javascript
Desktop.agentContact.addEventListener(
  "eResumeRecording",
  (msg) => console.log(msg)
);
```

For more information on example response, see [resumeRecording](https://developer.webex.com/docs/desktop-call-control#resumerecording).

#### ePauseRecording

Pauses a call recording for an accepted task or contact.

**Example**

```javascript
Desktop.agentContact.addEventListener(
  "ePauseRecording",
  (msg) => console.log(msg)
);
```

For more information on example response, see [pauseRecording](https://developer.webex.com/docs/desktop-call-control#pauserecording).

#### eConsultTransfer

Consult transfer request for an accepted task or contact.

**Example**

```javascript
Desktop.agentContact.addEventListener(
  "eConsultTransfer",
  (msg) => console.log(msg)
);
```

For more information on example response, see [consultTransfer](https://developer.webex.com/docs/desktop-transfers#consulttransfer).

#### eAgentblindTransferred

Transfers an accepted task or contact to an agent or queue.

**Example**

```javascript
Desktop.agentContact.addEventListener(
  "eAgentblindTransferred",
  (msg) => console.log(msg)
);
```

For more information on example response, see [blindTransfer](https://developer.webex.com/docs/desktop-transfers#blindtransfer).

#### eAgentvteamTransfer

Transfers an accepted task or contact to a queue.

**Example**

```javascript
Desktop.agentContact.addEventListener(
  "eAgentvteamTransfer",
  (msg) => console.log(msg)
);
```

For more information on example response, see [vTeamTransfer](https://developer.webex.com/docs/desktop-transfers#vteamtransfer).

#### eAgentConsultCreated

Consult request for an accepted task or contact has been created.

**Example**

```javascript
Desktop.agentContact.addEventListener(
  "eAgentConsultCreated",
  (msg) => console.log(msg)
);
```

For more information on example response, see [consult](https://developer.webex.com/docs/desktop-consultation-conferences#consult).

#### eAgentConsultConferenced

Consult conference request for an accepted task or contact has been connected.

**Note:** Event is received when conference is established for all channels except email.

**Example**

```javascript
Desktop.agentContact.addEventListener(
  "eAgentConsultConferenced",
  (msg) => console.log(msg)
);
```

For more information on example response, see [consultConference](https://developer.webex.com/docs/desktop-consultation-conferences#consultconference).

#### eAgentConsultEnded

Consult request for an accepted task or contact has ended.

**Example**

```javascript
Desktop.agentContact.addEventListener(
  "eAgentConsultEnded",
  (msg) => console.log(msg)
);
```

For more information on example response, see [consultEnd](https://developer.webex.com/docs/desktop-consultation-conferences#consultend).

#### eAgentCtqCancelled

Consult request to the queue has been canceled.

**Example**

```javascript
Desktop.agentContact.addEventListener(
  "eAgentCtqCancelled",
  (msg) => console.log(msg)
);
```

For more information on example response, see [cancelCtq](https://developer.webex.com/docs/desktop-consultation-conferences#cancelctq).

#### eAgentConsultConferenceEnded

Consult conference request for an accepted task or contact has ended.

**Example**

```javascript
Desktop.agentContact.addEventListener(
  "eAgentConsultConferenceEnded",
  (msg) => console.log(msg)
);
```

For more information on example response, see [consultEnd](https://developer.webex.com/docs/desktop-consultation-conferences#consultend).

#### eAgentConsulting

Agent has started consulting an incoming task or contact.

**Example**

```javascript
Desktop.agentContact.addEventListener(
  "eAgentConsulting",
  (msg) => console.log(msg)
);
```

For more information on example response, see [consultAccept](https://developer.webex.com/docs/desktop-consultation-conferences#consultaccept).

#### eAgentConsultFailed

Consult request for an accepted task or contact did not succeed.

**Example**

```javascript
Desktop.agentContact.addEventListener(
  "eAgentConsultFailed",
  (msg) => console.log(msg)
);
```

For more information on example response, see [consult](https://developer.webex.com/docs/desktop-consultation-conferences#consult).

#### eAgentConsultEndFailed

Request to end consult for an accepted task or contact did not succeed.

**Example**

```javascript
Desktop.agentContact.addEventListener(
  "eAgentConsultEndFailed",
  (msg) => console.log(msg)
);
```

For more information on example response, see [consultEnd](https://developer.webex.com/docs/desktop-consultation-conferences#consultend).

#### eAgentCtqFailed

Consult request to the queue did not succeed.

**Example**

```javascript
Desktop.agentContact.addEventListener(
  "eAgentCtqFailed",
  (msg) => console.log(msg)
);
```

For more information on example response, see [consult](https://developer.webex.com/docs/desktop-consultation-conferences#consult).

#### eAgentCtqCancelFailed

Request to cancel the consult to the queue did not succeed.

**Example**

```javascript
Desktop.agentContact.addEventListener(
  "eAgentCtqCancelFailed",
  (msg) => console.log(msg)
);
```

For more information on example response, see [cancelCtq](https://developer.webex.com/docs/desktop-consultation-conferences#cancelctq).

#### eAgentConsultConferenceEndFailed

Request to end the consult conference request did not succeed.

**Example**

```javascript
Desktop.agentContact.addEventListener(
  "eAgentConsultConferenceEndFailed",
  (msg) => console.log(msg)
);
```

#### eAgentMonitorStateChanged

The agent listens to this event when supervisor barges in to the interaction between the agent and customer.

**Example**

```javascript
Desktop.agentContact.addEventListener(
  "eAgentMonitorStateChanged",
  (msg) => console.log(msg)
);
```

#### eAgentMonitoringEnded

The agent listens to this event when supervisor has ended the call monitoring.

**Example**

```javascript
Desktop.agentContact.addEventListener(
  "eAgentMonitoringEnded",
  (msg) => console.log(msg)
);
```

#### eAgentOfferCampaignReserved

The agent listens to this event when the progressive campaign reservation call is ringing in the agent's device.

**Example**

```javascript
Desktop.agentContact.addEventListener(
  "eAgentOfferCampaignReserved",
  msg => console.log(msg)
);
```

#### eAgentAddCampaignReserved

The agent listens to this event when the agents answers the progressive campaign reservation call.

**Example**

```javascript
Desktop.agentContact.addEventListener(
  "eAgentAddCampaignReserved",
  msg => console.log(msg)
);
```

#### eAgentContactEnded

Occurs when a contact ends. Register a listener while the widget is mounted and remove the same handler during cleanup. See the [endV2 response](https://developer.webex.com/docs/desktop-call-control#endv2) for an example of the routing message with `data.type: "ContactEnded"` and the ended interaction's identifier.

```javascript
const onContactEnded = (message) => console.log("Contact ended:", message);
Desktop.agentContact.addEventListener("eAgentContactEnded", onContactEnded);

// During widget cleanup:
function cleanupEndedListener() {
  Desktop.agentContact.removeEventListener("eAgentContactEnded", onContactEnded);
}
```

#### eParticipantLeftConference

Occurs when a participant leaves a conference, including a successful `dropConferenceParticipant` request. The routing message's `data` includes `participantId`, `participantType`, `interactionId`, and `type: "ParticipantLeftConference"`; use those fields to identify the participant and interaction that changed. See the [conference participant removal response](https://developer.webex.com/docs/desktop-consultation-conferences#dropconferenceparticipant) for a complete example.

```javascript
const onParticipantLeft = (message) => {
  console.log("Conference participant left:", message.data);
};
Desktop.agentContact.addEventListener("eParticipantLeftConference", onParticipantLeft);

// Remove the listener when the widget disconnects.
function cleanupParticipantListener() {
  Desktop.agentContact.removeEventListener("eParticipantLeftConference", onParticipantLeft);
}
```

## Additional Contact Events in SDK 3

The SDK 3.0.1 declarations also expose the following events. Their callback payload uses `Service.Aqm.Contact.AgentContact` from the SDK types package; TypeScript infers the payload when you pass a callback to `addEventListener`. Inspect the fields supplied for the event before reading optional data.

### eAgentCampaignContactUpdated

Campaign contact information changes. Use the payload to refresh campaign-related widget data. Subscribe with `Desktop.agentContact.addEventListener("eAgentCampaignContactUpdated", handler)` and remove the same handler when the widget disconnects.

### eContactOwnerChanged

Contact ownership changes. The payload may include `fromOwner` and `toOwner` identifiers. Subscribe with `Desktop.agentContact.addEventListener("eContactOwnerChanged", handler)` and remove the same handler when the widget disconnects.

### eParticipantJoinedConference

A participant joins a conference. The payload may include the joined `participantId`. Subscribe with `Desktop.agentContact.addEventListener("eParticipantJoinedConference", handler)` and remove the same handler when the widget disconnects.

### eAgentConsultConferencing

A consultation is transitioning to a conference. Subscribe with `Desktop.agentContact.addEventListener("eAgentConsultConferencing", handler)` and remove the same handler when the widget disconnects.

### eAgentConsultTransferring

A consultation is transitioning to a transfer. Subscribe with `Desktop.agentContact.addEventListener("eAgentConsultTransferring", handler)` and remove the same handler when the widget disconnects.

## Related Pages

- [Agent Desktop overview](https://developer.webex.com/docs/desktop)
- [Desktop SDK Reference](https://developer.webex.com/docs/desktop-sdk-reference)
