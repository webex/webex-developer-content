---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-contact-events
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Asynchronous Events
- Contact Event Catalog
- eAgentContactAniUpdated
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
