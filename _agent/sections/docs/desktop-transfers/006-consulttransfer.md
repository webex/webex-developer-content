---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-transfers
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Agent Contact Methods
- consultTransfer()
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/desktop-transfers). [Full Markdown](../../../../docs/desktop-transfers.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before You Begin](001-before-you-begin.md)

## Article introduction

Transfer interactions to agents, dial numbers, and queues with the Desktop SDK.

## Parent context

## Agent Contact Methods

These methods belong to `Desktop.agentContact`. Use the V2 method where the older method is marked for deprecation.

## Selected section

### consultTransfer()

**Caution:** This method will be deprecated in the future.

Initiates a consult transfer request.

**Example**

```javascript
await Desktop.agentContact.consultTransfer({
    interactionId: "5c3d487a-874b-447d-b5f2-ce1f626301f5",
    data: {
        agentId: "43bfcdef-5551-45b1-a8f9-a0b33e66e3fe",
        destAgentId: "f795f41f-3782-44fa-97a4-c8b4dc029477",
        mediaType: "telephony",
        mediaResourceId: "b102ed10-fac2-4f8e-bece-1c2da6ba6dd8",
        destinationType: "Agent",
    }
});
```

**Payload type**

```typescript
type RequestPayload = {
    interactionId: string;data: Contact.consultTransferPayLoad
}

type consultTransferPayLoad = {
    agentId ?: string | undefined;
    destAgentId: string;
    mediaType: string;
    mediaResourceId: string;
    destinationType ?: string | undefined;
};
```

The following table lists the payload details:

| Name               | Type   | Description                                                                                         | Required |
| ------------------ | ------ | --------------------------------------------------------------------------------------------------- | -------- |
| interactionId      | String | Unique identifier for the user interaction.                                                         | Yes      |
| data               | Object | Options of the consult transfer request.                                                            | Yes      |
| -->agentId         | String | Unique identifier of the agent.                                                                     | Yes      |
| -->destAgentId     | String | Unique identifier of the consult transfer request destination agent.                                | Yes      |
| -->mediaType       | String | The media channel type such as telephony.                                                           | Yes      |
| -->mediaResourceId | String | Unique identifier of the media resource.                                                            | Yes      |
| -->destinationType | String | The type of consult transfer request to be placed. The destination type can be Agent, Queue, or DN. | Yes      |

**Returns**
`{Object}` The object with the retrieved data.

**Note:** The `type` parameter value in the response payload depends on the success or failure of the method. If the method is successful, the value is `AgentConsultTransferred`; else, `AgentConsultTransferFailed`.

**Example Response**

```javascript
const consultTransferResponse = {
  data: {
    agentId: "ff7dbe19-fa3f-4c63-8a1c-04dcffef8e4f",
    consultMediaResourceId: "fd0af60c-3250-46c3-96f8-1921f6ecf170",
    destAgentId: "9b036d89-930c-4187-a5bd-5dbb1439fe41",
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
          holdTimestamp: null,
          isHold: false,
          mType: "mainCall",
          mediaMgr: "vmm",
          mediaResourceId: "1277da79-dc49-439c-ab72-f00453a1ff71",
          mediaType: "telephony",
          participants: ["**********", "9b036d89-930c-4187-a5bd-5dbb1439fe41"]
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
          consultState: null,
          consultTimestamp: null,
          dn: "**********",
          hasJoined: true,
          id: "9b036d89-930c-4187-a5bd-5dbb1439fe41",
          isConsulted: true,
          isWrapUp: false,
          joinTimestamp: 1612429549032,
          lastUpdated: 1612429549032,
          name: "qaus1-gt-user1 qaus1-gt-user1",
          pType: "Agent",
          queueId: "1336",
          queueMgrId: "aqm",
          sessionId: "90896c91-0f77-4bc6-aec3-488a34ca88d3",
          siteId: "205",
          teamId: "598",
          teamName: "Sales",
          type: "Agent",
          wrapUpTimestamp: null
        },
        "ff7dbe19-fa3f-4c63-8a1c-04dcffef8e4f": {
          channelId: "fb704337-71c3-4802-a03b-84a2d18eeaa0",
          consultState: "consulting",
          consultTimestamp: 1612429549052,
          dn: "**********",
          hasJoined: true,
          id: "ff7dbe19-fa3f-4c63-8a1c-04dcffef8e4f",
          isConsulted: false,
          isWrapUp: false,
          joinTimestamp: 1612429537991,
          lastUpdated: 1612429537991,
          name: "qaus1-gt-user2 q",
          pType: "Agent",
          queueId: "1336",
          queueMgrId: "aqm",
          sessionId: "57323f8b-9460-45fa-aaf6-4ca51c327af8",
          siteId: "205",
          teamId: "598",
          teamName: "Sales",
          type: "Agent",
          wrapUpTimestamp: null
        }
      },
      previousVTeams: ["AW6h1AVRrZSGni185x28"],
      state: "connected",
      workflowManager: null
    },
    interactionId: "1277da79-dc49-439c-ab72-f00453a1ff71",
    mediaResourceId: "1277da79-dc49-439c-ab72-f00453a1ff71",
    orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
    queueMgr: "aqm",
    trackingId: "05b38615-5bdc-4e1d-8efe-60ea1c70fd5c",
    transferredMediaResourceId: "1277da79-dc49-439c-ab72-f00453a1ff71",
    type: "AgentConsultTransferred"
  },
  orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
  trackingId: "notifs_3464be63-83e7-4b2d-94d5-a63fddc108d5",
  type: "RoutingMessage"
};
```
