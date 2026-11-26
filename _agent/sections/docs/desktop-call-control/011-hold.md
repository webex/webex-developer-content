---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-call-control
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Agent Contact Methods
- hold()
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/desktop-call-control). [Full Markdown](../../../../docs/desktop-call-control.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before You Begin](001-before-you-begin.md)

## Article introduction

Retrieve tasks and control interactions, WebRTC calls, and call recording from Desktop widgets.

## Parent context

## Agent Contact Methods

These methods belong to `Desktop.agentContact`. Use the V2 method where the older method is marked for deprecation.

## Selected section

### hold()

Places a voice call on hold.

**Example**

```javascript
await Desktop.agentContact.hold({
    interactionId: "c837e6f7-699a-4736-bb82-03a6d58bb7f3",
    data: {
        mediaResourceId: "c837e6f7-699a-4736-bb82-03a6d58bb7f3"
    }
});

```

**Payload type**

```typescript
type HoldPayload = {
    interactionId: string;
    data: { mediaResourceId: string };
};
```

The following table lists the payload details:

| Name               | Type   | Description                                 | Required |
| ------------------ | ------ | ------------------------------------------- | -------- |
| interactionId      | String | Unique identifier for the user interaction. | Yes      |
| data               | Object | Options to place the voice call on hold.    | Yes      |
| -->mediaResourceId | String | Unique identifier of the media resource.    | Yes      |

**Returns**
`{Object}` The object with the retrieved data.

**Note:** The `type` parameter value in the response payload depends on the success or failure of the method. If the method is successful, the value is `AgentContactHeld`; else, `AgentContactHoldFailed`.

**Example Response**

```javascript
const holdResponse = {
  data: {
    agentId: "7c867aa9-ec768-341a-b767-e5hd6ae7g701",
    destAgentId: null,
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
        isPaused: "false",
        outdialTransferToQueueEnabled: "false",
        pauseDuration: "10",
        pauseResumeEnabled: "true",
        recordInProgress: "true",
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
      interactionId: "1dd08726-bca5-4ce8-9b51-b20dca8ab154",
      isFcManaged: false,
      isTerminated: false,
      media: {
        "1dd08726-bca5-4ce8-9b51-b20dca8ab154": {
          holdTimestamp: 1612355834441,
          isHold: true,
          mType: "mainCall",
          mediaMgr: "vmm",
          mediaResourceId: "1dd08726-bca5-4ce8-9b51-b20dca8ab154",
          mediaType: "telephony",
          participants: [""]
        }
      },
      mediaChannel: "dialer",
      mediaType: "telephony",
      orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
      outboundType: "OUTDIAL",
      owner: "7c867aa9-ec768-341a-b767-e5hd6ae7g701",
      participants: {
        "": {
          id: "",
          pType: "Customer",
          type: "Customer"
        },
        "7c867aa9-ec768-341a-b767-e5hd6ae7g701": {
          channelId: "0717a2ce-76cd-4ba4-9053-71f2c78168b8",
          consultState: null,
          consultTimestamp: null,
          dn: "8895579172",
          hasJoined: true,
          id: "7c867aa9-ec768-341a-b767-e5hd6ae7g701",
          isConsulted: false,
          isWrapUp: false,
          joinTimestamp: 1612354635705,
          lastUpdated: 1612354635705,
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
      state: "connected",
      workflowManager: null
    },
    interactionId: "1dd08726-bca5-4ce8-9b51-b20dca8ab154",
    mediaResourceId: "1dd08726-bca5-4ce8-9b51-b20dca8ab154",
    orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
    queueMgr: "aqm",
    trackingId: "3768264d-8588-465f-9ee6-0c25418ea9f7",
    type: "AgentContactHeld"
  },
  orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
  trackingId: "notifs_8e8cabb7-6d5a-460d-9b8b-ecfad96448b3",
  type: "RoutingMessage"
};
```
