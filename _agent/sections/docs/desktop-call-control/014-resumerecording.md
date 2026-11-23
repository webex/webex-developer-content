---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-call-control
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Agent Contact Methods
- resumeRecording()
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

### resumeRecording()

**Caution:** This method will be deprecated in the future.

Resumes a voice call recording that is paused.

**Example**

```javascript
await Desktop.agentContact.resumeRecording({
    interactionId: "c837e6f7-699a-4736-bb82-03a6d58bb7f3",
    data: {
        autoResumed: true
    }
});
// Resuming recording for telephony task
```

**Payload type**

```typescript
type RequestPayload = {
    interactionId: string;data: {
        autoResumed: boolean
    }
};
```

The following table lists the payload details:

| Name           | Type    | Description                                                                                                                                                                                                                                                      | Required |
| -------------- | ------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- |
| interactionId  | String  | Unique identifier for the user interaction.                                                                                                                                                                                                                      | Yes      |
| data           | Object  | Options to resume a voice call recording that is paused.                                                                                                                                                                                                         | Yes      |
| -->autoResumed | Boolean | Determines whether the paused call must be resumed manually.<br>True—Voice call to be resumed automatically after the specified time is lapsed.<br>False—User to take action on the paused voice call based on the button defined. For example, Start Recording. | Yes      |

**Returns**
`{Object}` The object with the retrieved data.

**Note:** The `type` parameter value in the response payload depends on the success or failure of the method. If the method is successful, the value is `ContactRecordingResumed`; else, `ContactRecordingResumeFailed`.

**Example Response**

```javascript
const resumeRecordingResponse = {
  data: {
    autoResumed: true,
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
          holdTimestamp: null,
          isHold: false,
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
    orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
    queueMgr: "aqm",
    trackingId: "9cf5bfc4-d120-4330-9996-039a9937c52c",
    type: "ContactRecordingResumed"
  },
  orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
  trackingId: "notifs_c04510a0-140a-439c-9ab4-68b6fdf6ea2e",
  type: "RoutingMessage"
};
```
