---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-contact-events
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Asynchronous Events
- Contact Event Catalog
- eCallRecordingStarted
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
