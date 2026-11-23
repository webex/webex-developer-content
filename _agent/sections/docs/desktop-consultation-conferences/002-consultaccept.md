---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-consultation-conferences
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Agent Contact Methods
- consultAccept()
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/desktop-consultation-conferences). [Full Markdown](../../../../docs/desktop-consultation-conferences.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before You Begin](001-before-you-begin.md)

## Article introduction

Use the Desktop SDK to consult agents and queues and manage conference participants.

## Parent context

## Agent Contact Methods

These methods belong to `Desktop.agentContact`. Use the V2 method where the older method is marked for deprecation.

## Selected section

### consultAccept()

Accepts a consult task.

**Example**

```javascript
await Desktop.agentContact.consultAccept({
    interactionId: "c837e6f7-699a-4736-bb82-03a6d58bb7f3"
});
```

The following table lists the payload details:

| Name          | Type   | Description                                 | Required |
| ------------- | ------ | ------------------------------------------- | -------- |
| interactionId | String | Unique identifier for the user interaction. | Yes      |

**Returns**

`{Object}` The value that corresponds to the task.

**Note:** The `type` parameter value in the response payload depends on the success or failure of the method. If the method is successful, the value is `AgentConsulting`; else, `AgentContactAssignFailed`.

**Example Response**

```javascript
const consultAcceptResponse = {
  data: {
    agentId: "9b036d89-930c-4187-a5bd-5dbb1439fe41",
    consultMediaResourceId: "c1b507d0-9aac-4500-a9f8-50f30eba4310",
    destAgentId: "ff7dbe19-fa3f-4c63-8a1c-04dcffef8e4f",
    destinationType: "Agent",
    eventType: "RoutingMessage",
    interaction: {
      callAssociatedData: {
        "": {
          agentEditable: false,
          displayName: "",
          name: "",
          type: "STRING",
          value: ""
        },
        IvrPath: {
          agentEditable: false,
          displayName: "IvrPath",
          name: "IvrPath",
          type: "STRING",
          value: " EOI"
        },
        ani: {
          agentEditable: false,
          displayName: "ani",
          name: "ani",
          type: "STRING",
          value: "**********"
        },
        dn: {
          agentEditable: false,
          displayName: "dn",
          name: "dn",
          type: "STRING",
          value: "**********"
        },
        nextVteamId: {
          agentEditable: false,
          displayName: "nextVteamId",
          name: "nextVteamId",
          type: "STRING",
          value: "Queue"
        },
        pathId: {
          agentEditable: false,
          displayName: "pathId",
          name: "pathId",
          type: "STRING",
          value: " StartCall PlayDone"
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
          value: "Queue-1"
        }
      },
      callAssociatedDetails: {
        "": "",
        IvrPath: " EOI",
        ani: "************",
        dn: "************",
        nextVteamId: "Queue",
        pathId: " StartCall PlayDone",
        ronaTimeout: "30",
        virtualTeamName: "Queue-1"
      },
      callFlowParams: {
        Queue: {
          description: "(vteam, A valid VTeam.)",
          name: "Queue",
          qualifier: "vteam",
          value: "1336",
          valueDataType: "string"
        },
        WelcomePrompt: {
          description: "(mediaFile, A valid media file.)",
          name: "WelcomePrompt",
          qualifier: "mediaFile",
          value: "GAwelcome.wav",
          valueDataType: "string"
        }
      },
      callProcessingDetails: {
        QMgrName: "aqm",
        QueueId: "1336",
        ani: "************",
        dnis: "************",
        isPaused: "false",
        jscriptId: "AW7HP3QNB44q0sL-cTVz",
        pauseDuration: "30",
        pauseResumeEnabled: "true",
        recordInProgress: "true",
        ronaTimeout: "30",
        taskToBeSelfServiced: "false",
        tenantId: "82",
        virtualTeamName: "Queue-1",
        vteamId: "1336"
      },
      contactDirection: {
        type: "INBOUND"
      },
      currentVTeam: "1336",
      interactionId: "1277da79-dc49-439c-ab72-f00453a1ff71",
      isFcManaged: false,
      isTerminated: false,
      media: {
        "1277da79-dc49-439c-ab72-f00453a1ff71": {
          holdTimestamp: 1612429578817,
          isHold: true,
          mType: "mainCall",
          mediaMgr: "vmm",
          mediaResourceId: "1277da79-dc49-439c-ab72-f00453a1ff71",
          mediaType: "telephony",
          participants: ["**********", "9b036d89-930c-4187-a5bd-5dbb1439fe41"]
        },
        "c1b507d0-9aac-4500-a9f8-50f30eba4310": {
          holdTimestamp: null,
          isHold: false,
          mType: "consult",
          mediaMgr: "vmm",
          mediaResourceId: "c1b507d0-9aac-4500-a9f8-50f30eba4310",
          mediaType: "telephony",
          participants: [
            "ff7dbe19-fa3f-4c63-8a1c-04dcffef8e4f",
            "9b036d89-930c-4187-a5bd-5dbb1439fe41",
            "ff7dbe19-fa3f-4c63-8a1c-04dcffef8e4f"
          ]
        }
      },
      mediaChannel: "broadcloud",
      mediaType: "telephony",
      orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
      outboundType: null,
      owner: "9b036d89-930c-4187-a5bd-5dbb1439fe41",
      participants: {
        "**********": {
          id: "**********",
          pType: "Customer",
          type: "Customer"
        },
        "9b036d89-930c-4187-a5bd-5dbb1439fe41": {
          channelId: "3de6706f-95b7-485a-9304-30928f7ee52e",
          consultState: "consulting",
          consultTimestamp: 1612429579220,
          dn: "**********",
          hasJoined: true,
          id: "9b036d89-930c-4187-a5bd-5dbb1439fe41",
          isConsulted: true,
          isWrapUp: false,
          joinTimestamp: 1612429549032,
          lastUpdated: 1612429549032,
          name: "user1",
          pType: "Agent",
          queueId: "1336",
          queueMgrId: "aqm",
          sessionId: "90896c91-0f77-4bc6-aec3-488a34ca88d3",
          siteId: "205",
          teamId: "598",
          teamName: "integ-test-team",
          type: "Agent",
          wrapUpTimestamp: null
        },
        "ff7dbe19-fa3f-4c63-8a1c-04dcffef8e4f": {
          channelId: "fb704337-71c3-4802-a03b-84a2d18eeaa0",
          consultState: "consulting",
          consultTimestamp: 1612429579220,
          dn: "**********",
          hasJoined: true,
          id: "ff7dbe19-fa3f-4c63-8a1c-04dcffef8e4f",
          isConsulted: true,
          isWrapUp: false,
          joinTimestamp: 1612429579200,
          lastUpdated: 1612429579200,
          name: "user2",
          pType: "Agent",
          queueId: "1336",
          queueMgrId: "aqm",
          sessionId: "57323f8b-9460-45fa-aaf6-4ca51c327af8",
          siteId: "205",
          teamId: "598",
          teamName: "integ-test-team",
          type: "Agent",
          wrapUpTimestamp: null
        }
      },
      previousVTeams: ["AW6h1AVRrZSGni185x28"],
      state: "consulting",
      workflowManager: null
    },
    interactionId: "1277da79-dc49-439c-ab72-f00453a1ff71",
    orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
    queueMgr: "aqm",
    trackingId: "e7c032be-b18e-4b63-8ab2-6baf50b137b1",
    type: "AgentConsulting"
  },
  orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
  trackingId: "notifs_3464be63-83e7-4b2d-94d5-a63fddc108d5",
  type: "RoutingMessage"
};
```
