---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-call-control
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Agent Contact Methods
- wrapupV2()
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

### wrapupV2()
Wraps up work for a task. Wrap up reason is applied after the task has been ended either by the agent or by the customer. A wrap up is essential and is the last step in an agent's flow of handling tasks.

**Example**

```javascript
await Desktop.agentContact.wrapupV2({
    interactionId: "dab1a2f0-bad0-11ea-8e7c-0d99ede2535a",
    data: {
        wrapUpReason: "Sales",
        auxCodeId: "AXUH3oN12eV-WekpnDpl",
        isAutoWrapup: false,
    }
});
```

**Payload type**

```typescript
type RequestPayload = {
    interactionId: string;data: Contact.WrapupPayLoad
};
```

The following table lists the payload details:

| Name            | Type    | Description                                                                                                                                | Required |
| --------------- | ------- | ------------------------------------------------------------------------------------------------------------------------------------------ | -------- |
| interactionId   | String  | Unique identifier for the user interaction.                                                                                                | Yes      |
| data            | Object  | Options of the wrap up.                                                                                                                    | Yes      |
| -->wrapUpReason | String  | Every wrap up reason will have an unique auxillary code. Use this field to specify the reason for wrapping up the call, maximum length 128 characters.                                                                        | Yes      |
| -->auxCodeId    | String  | Auxiliary codes are status codes which an agent can select in Webex Contact Center Agent Desktop. They are of two types: Idle and Wrap-Up codes, and every agent profile must have one of each for the agent to use.  Wrap-up codes indicate the result of customer contacts, such as successful resolution or escalation of the contact. Creating and managing auxiliary codes requires an administrator role and the appropriate cjp:config_write or cjp:config_read scopes, maximum length 36 characters.                                                                                                      | Yes      |
| -->isAutoWrapup | Boolean | Determines whether the auto wrap up is enabled or not.<br><br>- True—The auto warp up is enabled.<br>- False—The auto warp up is disabled. | Yes      |

**Returns**
`{Object}` The object with the retrieved data.

**Note:** The `type` parameter value in the response payload depends on the success or failure of the method. If the method is successful, the value is `AgentWrappedUp`; else, `AgentWrapupFailed`.

**Example Response**

```javascript
const wrapUpResponse = {
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
                "vteamId": "AXCqFyz1G2pKap9PI-mW"
            },
            "contactDirection": {
                "type": "INBOUND"
            },
            "currentVTeam": "3270",
            "interactionId": "a66d05ab-40ab-11eb-b59a-7d3326b3ffc1",
            "isFcManaged": false,
            "isTerminated": true,
            "media": {},
            "mediaChannel": "web",
            "mediaType": "chat",
            "orgId": "f111e3af-1a45-42ef-9erf-4562354b8a25",
            "outboundType": null,
            "owner": "7d12d9ea-e8e0-41ee-81bf-c11a685b64ed",
            "participants": {
                "janedoe@gmail.com": {
                    "id": "janedoe@gmail.com",
                    "pType": "Customer",
                    "type": "Customer"
                }
            },
            "previousVTeams": [],
            "state": "connected"
        },
        "interactionId": "a66d05ab-40ab-11eb-b59a-7d3326b3ffc1",
        "orgId": "f111e3af-1a45-42ef-9erf-4562354b8a25",
        "queueMgr": "aqm",
        "trackingId": "5272a610-40ac-11eb-8866-d7ef6ff89aa6",
        "type": "AgentWrappedUp",
        "wrapUpAuxCodeId": "0"
    },
    "orgId": "f111e3af-1a45-42ef-9erf-4562354b8a25",
    "trackingId": "notifs_b5e0ebb7-fd1d-479f-8663-81a64030cee6",
    "type": "RoutingMessage"
}
```
