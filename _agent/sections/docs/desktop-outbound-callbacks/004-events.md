---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-outbound-callbacks
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Dialer Module
- Events
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
