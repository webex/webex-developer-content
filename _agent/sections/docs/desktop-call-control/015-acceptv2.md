---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-call-control
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Agent Contact Methods
- acceptV2()
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

### acceptV2()
Accepts an incoming task.

**Note:** This method works only for non-voice tasks and isn't applicable for voice contacts.

**Example**

```javascript
await Desktop.agentContact.acceptV2({
    interactionId: "c837e6f7-699a-4736-bb82-03a6d58bb7f3"
});
```

The following table lists the payload details:

| Name          | Type   | Description                                 | Required |
| ------------- | ------ | ------------------------------------------- | -------- |
| interactionId | String | Unique identifier for the user interaction. | Yes      |

**Returns**

`{Object}` The value that corresponds to the task.

**Note:** The `type` parameter value in the response payload depends on the success or failure of the method. If the method is successful, the value is `AgentContactAssigned`; else, `AgentContactAssignFailed`.

**Example Response**

```javascript
const acceptResponse = {
  data: {
    agentId: "7d12d9ea-e8e0-41ee-81bf-c11a685b64ed",
    eventType: "RoutingMessage",
    interaction: {
      callAssociatedData: {
        ani: {
          value: "janedoe@gmail.com"
        },
        category: {
          value: "Sales"
        },
        customerName: {
          value: "Jane Doe"
        },
        dn: {
          value: "Desktop"
        },
        entryPointId: {
          value: "AXCqFyz1G2pKap9PI-mW"
        },
        guestId: {
          value:
            "Y2lzY29zcGFyazovL3VzL1BFT1BMRS83ZjA3YjJmMC1jNTMyLTQ5MDktYTkzNi0yYTA3MTVmZGIwMTA"
        },
        mediaChannel: {
          value: "web"
        },
        reason: {
          value: "Test"
        },
        reasonCode: {
          value: "Sales"
        },
        ronaTimeout: {
          value: "30"
        },
        roomTitle: {
          value: "Help Jane Doe with Sales"
        },
        taskToBeSelfServiced: {
          value: "false"
        },
        templateId: {
          value: "b57990c0-5ec6-11ea-96ee-5df5aef56329"
        },
        templateName: {
          value: "Desktop"
        },
        virtualTeamName: {
          value: "Chat_Queue"
        }
      },
      callAssociatedDetails: {
        ani: "janedoe@gmail.com",
        category: "Sales",
        customerName: "Jane Doe",
        dn: "Desktop",
        entryPointId: "AXCqFyz1G2pKap9PI-mW",
        guestId:
          "Y2lzY29zcGFyazovL3VzL1BFT1BMRS83ZjA3YjJmMC1jNTMyLTQ5MDktYTkzNi0yYTA3MTVmZGIwMTA",
        mediaChannel: "web",
        reason: "Test",
        reasonCode: "Sales",
        ronaTimeout: "30",
        roomTitle: "Help Jane Doe with Sales",
        taskToBeSelfServiced: "false",
        templateId: "b57990c0-5ec6-11ea-96ee-5df5aef56329",
        templateName: "Desktop",
        virtualTeamName: "Chat_Queue"
      },
      callFlowParams: {
        Automation: {
          description: "(vteam, A valid VTeam.)",
          name: "Automation",
          qualifier: "vteam",
          value: "3270",
          valueDataType: "string"
        },
        Debit: {
          description: "(vteam, A valid VTeam.)",
          name: "Debit",
          qualifier: "vteam",
          value: "3270",
          valueDataType: "string"
        },
        Sales: {
          description: "(vteam, A valid VTeam.)",
          name: "Sales",
          qualifier: "vteam",
          value: "3270",
          valueDataType: "string"
        }
      },
      callProcessingDetails: {
        QMgrName: "aqm",
        QueueId: "3270",
        ani: "janedoe@gmail.com",
        category: "Sales",
        customerName: "Jane Doe",
        dnis: "Desktop",
        entryPointId: "AXCqFyz1G2pKap9PI-mW",
        guestId:
          "Y2lzY29zcGFyazovL3VzL1BFT1BMRS83ZjA3YjJmMC1jNTMyLTQ5MDktYTkzNi0yYTA3MTVmZGIwMTA",
        mediaChannel: "web",
        reason: "Test",
        reasonCode: "Sales",
        ronaTimeout: "30",
        roomTitle: "Help Jane Doe with Sales",
        taskToBeSelfServiced: "false",
        templateId: "b57990c0-5ec6-11ea-96ee-5df5aef56329",
        templateName: "Desktop",
        tenantId: "133",
        virtualTeamName: "Chat_Queue",
        vteamId: "AXCqFyz1G2pKap9PI-mW"
      },
      contactDirection: {
        type: "INBOUND"
      },
      currentVTeam: "3270",
      interactionId: "59dbbca6-4194-11eb-881c-253923a967e0",
      isFcManaged: false,
      isTerminated: false,
      media: {
        Y2lzY29zcGFyazovL3VzL1JPT00vNjVjOWVlYjAtNDE5NC0xMWViLWE1N2QtZWY2N2MwZTMyYmFh:
          {
            holdTimestamp: null,
            isHold: false,
            mType: "mainCall",
            mediaMgr: "cmm",
            mediaResourceId:
              "Y2lzY29zcGFyazovL3VzL1JPT00vNjVjOWVlYjAtNDE5NC0xMWViLWE1N2QtZWY2N2MwZTMyYmFh",
            mediaType: "chat",
            participants: [
              "janedoe@gmail.com",
              "7d12d9ea-e8e0-41ee-81bf-c11a685b64ed"
            ]
          }
      },
      mediaChannel: "web",
      mediaType: "chat",
      orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
      outboundType: null,
      owner: "7d12d9ea-e8e0-41ee-81bf-c11a685b64ed",
      participants: {
        "7d12d9ea-e8e0-41ee-81bf-c11a685b64ed": {
          channelId: "bff9350a-9d2a-489a-a8d5-d9dacea4b692",
          consultState: null,
          consultTimestamp: null,
          dn: "9997770110",
          hasJoined: true,
          id: "7d12d9ea-e8e0-41ee-81bf-c11a685b64ed",
          isConsulted: false,
          isWrapUp: false,
          joinTimestamp: 1608339210824,
          lastUpdated: 1608339210824,
          name: "uuip-agent4 uuip-agent4",
          pType: "Agent",
          queueId: "3270",
          queueMgrId: "aqm",
          sessionId: "102d2096-bcc0-45bb-a583-a02f6c188071",
          siteId: "473",
          teamId: "1940",
          teamName: "Medical Help",
          type: "Agent",
          wrapUpTimestamp: null
        },
        "janedoe@gmail.com": {
          id: "janedoe@gmail.com",
          pType: "Customer",
          type: "Customer"
        }
      },
      previousVTeams: [],
      state: "connected"
    },
    interactionId: "59dbbca6-4194-11eb-881c-253923a967e0",
    mediaResourceId:
      "Y2lzY29zcGFyazovL3VzL1JPT00vNjVjOWVlYjAtNDE5NC0xMWViLWE1N2QtZWY2N2MwZTMyYmFh",
    orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
    queueMgr: "aqm",
    trackingId: "9c9b97e0-4194-11eb-b819-7b8dd50ee0cd",
    type: "AgentContactAssigned"
  },
  orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
  trackingId: "notifs_02db68c8-a5db-4028-95bb-1aebd6f87609",
  type: "RoutingMessage"
};
```
