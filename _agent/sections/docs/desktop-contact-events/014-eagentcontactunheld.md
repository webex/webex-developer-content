---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-contact-events
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Asynchronous Events
- Contact Event Catalog
- eAgentContactUnHeld
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
