---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-agent-state
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Desktop Actions
- getMediaTypeQueue(mediaType)
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/desktop-agent-state). [Full Markdown](../../../../docs/desktop-agent-state.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before You Begin](001-before-you-begin.md)

## Article introduction

Read agent information and manage availability by media channel with the Desktop SDK.

## Parent context

## Desktop Actions

Auxiliary-code pagination uses `Desktop.agentConfigJsApi`. The other methods in this section use `Desktop.actions`.

## Selected section

### getMediaTypeQueue(mediaType)

Retrieves the current media queue for one channel type.

**Note:** The administrator configures the media type for an agent.

**Example**

```javascript
const queue = await Desktop.actions.getMediaTypeQueue("email"); // => Get current media queue from Desktop store
```

**Parameters**

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| mediaType | String | One media channel type: `telephony`, `social`, `email`, or `chat`. Social includes Messenger and SMS. | Yes |

**Returns**
`{Object}` The object with the retrieved data.

**Example Response**

```json
{
    "key": "c9897fa7-6188-11eb-a6e4-f93bdeada4e5",
    "value": {
        "agentId": "7c867aa9-ec768-341a-b767-e5hd6ae7g701",
        "consultMediaResourceId": null,
        "eventType": "RoutingMessage",
        "interaction": {
            "callAssociatedData": {
                "accountId": {
                    "agentEditable": false,
                    "displayName": "accountId",
                    "name": "accountId",
                    "type": "STRING",
                    "value": "e9e2c7a0-5c64-11ea-9e59-6fbf992ffc23"
                },
                "ani": {
                    "agentEditable": false,
                    "displayName": "ani",
                    "name": "ani",
                    "type": "STRING",
                    "value": "janedoe@gmail.com"
                },
                "bccAddress": {
                    "agentEditable": false,
                    "displayName": "bccAddress",
                    "name": "bccAddress",
                    "type": "STRING",
                    "value": ""
                },
                "ccAddress": {
                    "agentEditable": false,
                    "displayName": "ccAddress",
                    "name": "ccAddress",
                    "type": "STRING",
                    "value": ""
                },
                "contentType": {
                    "agentEditable": false,
                    "displayName": "contentType",
                    "name": "contentType",
                    "type": "STRING",
                    "value": "multipart/alternative"
                },
                "customerName": {
                    "agentEditable": false,
                    "displayName": "customerName",
                    "name": "customerName",
                    "type": "STRING",
                    "value": "Jane Doe"
                },
                "date": {
                    "agentEditable": false,
                    "displayName": "date",
                    "name": "date",
                    "type": "STRING",
                    "value": "Wed, 20 Jan 2021 06:09:06 +0000"
                },
                "dn": {
                    "agentEditable": false,
                    "displayName": "dn",
                    "name": "dn",
                    "type": "STRING",
                    "value": "agent2021@gmail.com"
                },
                "entryPointId": {
                    "agentEditable": false,
                    "displayName": "entryPointId",
                    "name": "entryPointId",
                    "type": "STRING",
                    "value": "AXCZuH9MXrf9I0XFBIfL"
                },
                "from": {
                    "agentEditable": false,
                    "displayName": "from",
                    "name": "from",
                    "type": "STRING",
                    "value": "Jane Doe"
                },
                "fromAddress": {
                    "agentEditable": false,
                    "displayName": "fromAddress",
                    "name": "fromAddress",
                    "type": "STRING",
                    "value": "janedoe@gmail.com"
                },
                "inReplyTo": {
                    "agentEditable": false,
                    "displayName": "inReplyTo",
                    "name": "inReplyTo",
                    "type": "STRING",
                    "value": ""
                },
                "messageId": {
                    "agentEditable": false,
                    "displayName": "messageId",
                    "name": "messageId",
                    "type": "STRING",
                    "value": "289DBEAD-0715-4878-A0B9-365555C18E72@cisco.com"
                },
                "queueType": {
                    "agentEditable": false,
                    "displayName": "queueType",
                    "name": "queueType",
                    "type": "STRING",
                    "value": "tam"
                },
                "reasonCode": {
                    "agentEditable": false,
                    "displayName": "reasonCode",
                    "name": "reasonCode",
                    "type": "STRING",
                    "value": "Email_Queue"
                },
                "references": {
                    "agentEditable": false,
                    "displayName": "references",
                    "name": "references",
                    "type": "STRING",
                    "value": ""
                },
                "replyToAddress": {
                    "agentEditable": false,
                    "displayName": "replyToAddress",
                    "name": "replyToAddress",
                    "type": "STRING",
                    "value": "janedoe@gmail.com"
                },
                "ronaTimeout": {
                    "agentEditable": false,
                    "displayName": "ronaTimeout",
                    "name": "ronaTimeout",
                    "type": "STRING",
                    "value": "30"
                },
                "subject": {
                    "agentEditable": false,
                    "displayName": "subject",
                    "name": "subject",
                    "type": "STRING",
                    "value": "sales"
                },
                "threadId": {
                    "agentEditable": false,
                    "displayName": "threadId",
                    "name": "threadId",
                    "type": "STRING",
                    "value": "289DBEAD-0715-4878-A0B9-365555C18E72@cisco.com"
                },
                "toAddress": {
                    "agentEditable": false,
                    "displayName": "toAddress",
                    "name": "toAddress",
                    "type": "STRING",
                    "value": "agent2021@gmail.com"
                },
                "virtualTeamName": {
                    "agentEditable": false,
                    "displayName": "virtualTeamName",
                    "name": "virtualTeamName",
                    "type": "STRING",
                    "value": "Email_Queue"
                }
            },
            "callAssociatedDetails": {
                "accountId": "e9e2c7a0-5c64-11ea-9e59-6fbf992ffc23",
                "ani": "janedoe@gmail.com",
                "bccAddress": "",
                "ccAddress": "",
                "contentType": "multipart/alternative",
                "customerName": "Jane Doe",
                "date": "Wed, 20 Jan 2021 06:09:06 +0000",
                "dn": "agent2021@gmail.com",
                "entryPointId": "AXCZuH9MXrf9I0XFBIfL",
                "from": "Jane Doe",
                "fromAddress": "janedoe@gmail.com",
                "inReplyTo": "",
                "messageId": "289DBEAD-0715-4878-A0B9-365555C18E72@cisco.com",
                "queueType": "tam",
                "reasonCode": "Email_Queue",
                "references": "",
                "replyToAddress": "janedoe@gmail.com",
                "ronaTimeout": "30",
                "subject": "sales",
                "threadId": "289DBEAD-0715-4878-A0B9-365555C18E72@cisco.com",
                "toAddress": "agent2021@gmail.com",
                "virtualTeamName": "Email_Queue"
            },
            "callFlowParams": {
                "Automation_Email_Queue": {
                    "description": "",
                    "name": "Automation_Email_Queue",
                    "qualifier": "vteam",
                    "value": "3281",
                    "valueDataType": "string"
                },
                "Dont_Use_Email": {
                    "description": "",
                    "name": "Dont_Use_Email",
                    "qualifier": "vteam",
                    "value": "3276",
                    "valueDataType": "string"
                },
                "Email_Queue": {
                    "description": "",
                    "name": "Email_Queue",
                    "qualifier": "vteam",
                    "value": "3266",
                    "valueDataType": "string"
                },
                "Mail_Automation_Queue": {
                    "description": "",
                    "name": "Mail_Automation_Queue",
                    "qualifier": "vteam",
                    "value": "3432",
                    "valueDataType": "string"
                }
            },
            "callProcessingDetails": {
                "QMgrName": "aqm",
                "QueueId": "3266",
                "accountId": "e9e2c7a0-5c64-11ea-9e59-6fbf992ffc23",
                "ani": "janedoe@gmail.com",
                "bccAddress": "",
                "ccAddress": "",
                "contentType": "multipart/alternative",
                "customerName": "Jane Doe",
                "date": "Wed, 20 Jan 2021 06:09:06 +0000",
                "dnis": "agent2021@gmail.com",
                "entryPointId": "AXCZuH9MXrf9I0XFBIfL",
                "from": "Jane Doe",
                "fromAddress": "janedoe@gmail.com",
                "inReplyTo": "",
                "messageId": "289DBEAD-0715-4878-A0B9-365555C18E72@cisco.com",
                "pauseDuration": "10",
                "pauseResumeEnabled": "true",
                "queueType": "tam",
                "reasonCode": "Email_Queue",
                "references": "",
                "replyToAddress": "janedoe@gmail.com",
                "ronaTimeout": "30",
                "subject": "sales",
                "taskToBeSelfServiced": "false",
                "tenantId": "133",
                "threadId": "289DBEAD-0715-4878-A0B9-365555C18E72@cisco.com",
                "toAddress": "agent2021@gmail.com",
                "virtualTeamName": "Email_Queue",
                "vteamId": "AXCZuH9MXrf9I0XFBIfL"
            },
            "contactDirection": {
                "type": "INBOUND"
            },
            "currentVTeam": "3266",
            "interactionId": "c9897fa7-6188-11eb-a6e4-f93bdeada4e5",
            "isFcManaged": false,
            "isTerminated": false,
            "media": {
                "289DBEAD-0715-4878-A0B9-365555C18E72@cisco.com": {
                    "holdTimestamp": null,
                    "isHold": false,
                    "mType": "mainCall",
                    "mediaMgr": "emm",
                    "mediaResourceId": "289DBEAD-0715-4878-A0B9-365555C18E72@cisco.com",
                    "mediaType": "email",
                    "participants": [
                        "janedoe@gmail.com",
                        "7c867aa9-ec768-341a-b767-e5hd6ae7g701"
                    ]
                }
            },
            "mediaChannel": "email",
            "mediaType": "email",
            "orgId": "f111e3af-1a45-42ef-9erf-4562354b8a25",
            "outboundType": null,
            "owner": "7c867aa9-ec768-341a-b767-e5hd6ae7g701",
            "participants": {
                "7c867aa9-ec768-341a-b767-e5hd6ae7g701": {
                    "channelId": "a72a75f8-fd30-44f9-85f1-39d633055475",
                    "consultState": null,
                    "consultTimestamp": null,
                    "dn": "8895579172",
                    "hasJoined": true,
                    "id": "7c867aa9-ec768-341a-b767-e5hd6ae7g701",
                    "isConsulted": false,
                    "isWrapUp": false,
                    "joinTimestamp": 1612248681335,
                    "lastUpdated": 1612248681336,
                    "name": "John Doe",
                    "pType": "Agent",
                    "queueId": "3266",
                    "queueMgrId": "aqm",
                    "sessionId": "3d017488-527a-4e89-9313-5d4eb353c789",
                    "siteId": "472",
                    "teamId": "960",
                    "teamName": "Email_Team",
                    "type": "Agent",
                    "wrapUpTimestamp": null
                },
                "janedoe@gmail.com": {
                    "id": "janedoe@gmail.com",
                    "pType": "Customer",
                    "type": "Customer"
                }
            },
            "previousVTeams": [],
            "state": "connected",
            "workflowManager": null
        },
        "interactionId": "c9897fa7-6188-11eb-a6e4-f93bdeada4e5",
        "isConsulted": false,
        "mediaResourceId": "289DBEAD-0715-4878-A0B9-365555C18E72@cisco.com",
        "orgId": "f111e3af-1a45-42ef-9erf-4562354b8a25",
        "queueMgr": "aqm",
        "trackingId": "2e30a830-6611-11eb-bbe4-81e078594d7a",
        "type": "AgentContact"
    }
}
```
