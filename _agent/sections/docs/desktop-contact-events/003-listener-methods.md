---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-contact-events
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Asynchronous Events
- Listener Methods
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

## Selected section

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
