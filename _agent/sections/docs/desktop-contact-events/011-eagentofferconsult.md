---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-contact-events
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Asynchronous Events
- Contact Event Catalog
- eAgentOfferConsult
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
