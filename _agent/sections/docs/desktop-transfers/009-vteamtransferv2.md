---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-transfers
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Agent Contact Methods
- vTeamTransferV2()
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

### vTeamTransferV2()

Initiates a vTeam transfer request.

**Example**

```javascript
await Desktop.agentContact.vteamTransferV2({
    interactionId: "dab1a2f0-bad0-11ea-8e7c-0d99ede2535a",
    data: {
        to: "AXDiuOLjKin42Ov3QJXN",
        destinationType: "queue"
    }
});
```

**Payload type**

```typescript
type RequestPayload = {
    interactionId: string;
    data: Contact.vteamTransferV2PayLoad
}

type vteamTransferV2PayLoad = {
    to: string;
    destinationType: string;
};
```

The following table lists the payload details:

| Name          | Type   | Description                                                                                                                                    | Required |
| ------------- | ------ | ---------------------------------------------------------------------------------------------------------------------------------------------- | -------- |
| interactionId | String | Unique identifier for the user interaction.                                                                                                    | Yes      |
| data          | Object | Options of the vTeam transfer request.                                                                                                         | Yes      |
| -->to    | String | vTeam unique identifier.                                                                                                                       | Yes      |
| -->destinationType  | String | vTeam transfer type. The user can transfer to another user in the team(agent), queue(queue), dial number(dialNumber), entry point(entrypointDialNumber). | Yes      |

**Returns**
`{Object}` The object with the retrieved data.

**Note:** The `type` parameter value in the response payload depends on the success or failure of the method. If the method is successful, the value is `AgentVteamTransferred`; else, `AgentVteamTransferFailed`.

**Example Response**

```javascript
const vTeamTransferResponse = {
    "data": {
        "agentId": "7d12d9ea-e8e0-41ee-81bf-c11a685b64ed",
        "eventType": "RoutingMessage",
        "interaction": {
            "callAssociatedData": {
                "ani": {
                    "value": "janedoe@gmail.com"
                },
                "category": {
                    "value": "Sales"
                },
                "customerName": {
                    "value": "Jane Doe"
                },
                "dn": {
                    "value": "Desktop"
                },
                "entryPointId": {
                    "value": "AXCqFyz1G2pKap9PI-mW"
                },
                "guestId": {
                    "value": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS81NzNiODg1Mi1kZjM3LTRlODEtOGMxMi1mZjkyMTE3MmQ1NzY"
                },
                "mediaChannel": {
                    "value": "web"
                },
                "reason": {
                    "value": "Test"
                },
                "reasonCode": {
                    "value": "Sales"
                },
                "ronaTimeout": {
                    "value": "30"
                },
                "roomTitle": {
                    "value": "Help Jane Doe with Sales"
                },
                "taskToBeSelfServiced": {
                    "value": "false"
                },
                "templateId": {
                    "value": "b57990c0-5ec6-11ea-96ee-5df5aef56329"
                },
                "templateName": {
                    "value": "Desktop"
                },
                "virtualTeamName": {
                    "value": "Chat_Queue"
                }
            },
            "callAssociatedDetails": {
                "ani": "janedoe@gmail.com",
                "category": "Sales",
                "customerName": "Jane Doe",
                "dn": "Desktop",
                "entryPointId": "AXCqFyz1G2pKap9PI-mW",
                "guestId": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS81NzNiODg1Mi1kZjM3LTRlODEtOGMxMi1mZjkyMTE3MmQ1NzY",
                "mediaChannel": "web",
                "reason": "Test",
                "reasonCode": "Sales",
                "ronaTimeout": "30",
                "roomTitle": "Help Jane Doe with Sales",
                "taskToBeSelfServiced": "false",
                "templateId": "b57990c0-5ec6-11ea-96ee-5df5aef56329",
                "templateName": "Desktop",
                "virtualTeamName": "Chat_Queue"
            },
            "callFlowParams": {
                "Automation": {
                    "description": "(vteam, A valid VTeam.)",
                    "name": "Automation",
                    "qualifier": "vteam",
                    "value": "3270",
                    "valueDataType": "string"
                },
                "Debit": {
                    "description": "(vteam, A valid VTeam.)",
                    "name": "Debit",
                    "qualifier": "vteam",
                    "value": "3270",
                    "valueDataType": "string"
                },
                "Sales": {
                    "description": "(vteam, A valid VTeam.)",
                    "name": "Sales",
                    "qualifier": "vteam",
                    "value": "3270",
                    "valueDataType": "string"
                }
            },
            "callProcessingDetails": {
                "QMgrName": "aqm",
                "QueueId": "3270",
                "ani": "janedoe@gmail.com",
                "category": "Sales",
                "customerName": "Jane Doe",
                "dnis": "Desktop",
                "doNotRouteToAgents": "7d12d9ea-e8e0-41ee-81bf-c11a685b64ed",
                "entryPointId": "AXCqFyz1G2pKap9PI-mW",
                "guestId": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS81NzNiODg1Mi1kZjM3LTRlODEtOGMxMi1mZjkyMTE3MmQ1NzY",
                "mediaChannel": "web",
                "pauseDuration": "10",
                "pauseResumeEnabled": "true",
                "reason": "Test",
                "reasonCode": "Sales",
                "ronaTimeout": "30",
                "roomTitle": "Help Jane Doe with Sales",
                "taskToBeSelfServiced": "false",
                "templateId": "b57990c0-5ec6-11ea-96ee-5df5aef56329",
                "templateName": "Desktop",
                "tenantId": "133",
                "virtualTeamName": "Chat_Queue",
                "vteamId": "7178",
                "vteamType": "inboundqueue"
            },
            "contactDirection": {
                "type": "INBOUND"
            },
            "currentVTeam": "7178",
            "interactionId": "29bafa9c-40b5-11eb-8606-edd437f1b927",
            "isFcManaged": false,
            "isTerminated": false,
            "media": {
                "Y2lzY29zcGFyazovL3VzL1JPT00vMmNiMTMwMDAtNDBiNS0xMWViLWE4M2ItZWI4ZTQwMDk1MDk5": {
                    "holdTimestamp": null,
                    "isHold": false,
                    "mType": "mainCall",
                    "mediaMgr": "cmm",
                    "mediaResourceId": "Y2lzY29zcGFyazovL3VzL1JPT00vMmNiMTMwMDAtNDBiNS0xMWViLWE4M2ItZWI4ZTQwMDk1MDk5",
                    "mediaType": "chat",
                    "participants": ["janedoe@gmail.com", "7d12d9ea-e8e0-41ee-81bf-c11a685b64ed"]
                }
            },
            "mediaChannel": "web",
            "mediaType": "chat",
            "orgId": "f111e3af-1a45-42ef-9erf-4562354b8a25",
            "outboundType": null,
            "owner": null,
            "participants": {
                "7d12d9ea-e8e0-41ee-81bf-c11a685b64ed": {
                    "channelId": "ccbffa6f-4322-4e06-850f-e0ab2915f238",
                    "consultState": null,
                    "consultTimestamp": null,
                    "dn": "9997770110",
                    "hasJoined": true,
                    "id": "7d12d9ea-e8e0-41ee-81bf-c11a685b64ed",
                    "isConsulted": false,
                    "isWrapUp": true,
                    "joinTimestamp": 1608243279477,
                    "lastUpdated": 1608254153975,
                    "name": "FirstName LastName",
                    "pType": "Agent",
                    "queueId": "3270",
                    "queueMgrId": "aqm",
                    "sessionId": "b8c096ab-f9a0-49be-9efd-f8c78e1a7061",
                    "siteId": "473",
                    "teamId": "962",
                    "teamName": "Team X",
                    "type": "Agent",
                    "wrapUpTimestamp": 1608254153975
                },
                "janedoe@gmail.com": {
                    "id": "janedoe@gmail.com",
                    "pType": "Customer",
                    "type": "Customer"
                }
            },
            "previousVTeams": ["3270"],
            "state": "new"
        },
        "interactionId": "29bafa9c-40b5-11eb-8606-edd437f1b927",
        "orgId": "f111e3af-1a45-42ef-9erf-4562354b8a25",
        "queueMgr": "aqm",
        "trackingId": "91480930-40ce-11eb-840f-7f9e29c6b481",
        "type": "AgentVteamTransferred"
    }
}
```
