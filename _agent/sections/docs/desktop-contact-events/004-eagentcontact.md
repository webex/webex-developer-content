---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-contact-events
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Asynchronous Events
- Contact Event Catalog
- eAgentContact
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/desktop-contact-events). [Full Markdown](../../../../docs/desktop-contact-events.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before You Begin](001-before-you-begin.md)

## Article introduction

Subscribe to Desktop contact events and use their payloads to keep widgets synchronized with interactions.

## Parent context

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

### Contact Event Catalog

## Selected section

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
