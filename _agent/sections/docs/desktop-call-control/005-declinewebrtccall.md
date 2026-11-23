---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-call-control
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Desktop Actions
- declineWebRtcCall()
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/desktop-call-control). [Full Markdown](../../../../docs/desktop-call-control.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before You Begin](001-before-you-begin.md)

## Article introduction

Retrieve tasks and control interactions, WebRTC calls, and call recording from Desktop widgets.

## Parent context

## Desktop Actions

The `Desktop.actions` module retrieves data and performs actions for Desktop widgets.

## Selected section

### declineWebRtcCall()

Declines an incoming WebRTC call. This method allows agents to reject WebRTC-based voice calls that are being offered.

**Example**

```javascript
await Desktop.actions.declineWebRtcCall();
// => Decline the incoming WebRTC call
```


**Example Response**

```json
{
    "data": {
        "agentId": "4f91ee74-9747-4c97-ae25-c2a753f2edb1",
        "agentSessionId": "89ad50c4-99f5-4c83-afb4-4f238d93b664",
        "eventTime": 1758824113184,
        "eventType": "RoutingMessage",
        "interaction": {
            "callAssociatedData": {
                "CallDate": {
                    "agentEditable": true,
                    "agentViewable": true,
                    "displayName": "CallDate",
                    "global": false,
                    "isSecure": false,
                    "name": "CallDate",
                    "reportable": false,
                    "secureKeyId": "",
                    "secureKeyVersion": 0,
                    "type": "DATETIME",
                    "value": "2025-09-25T18:15:02.534Z[UTC]"
                },
                "Customer_Name": {
                    "agentEditable": true,
                    "agentViewable": true,
                    "displayName": "Customer_Name",
                    "global": false,
                    "isSecure": false,
                    "name": "Customer_Name",
                    "reportable": false,
                    "secureKeyId": "",
                    "secureKeyVersion": 0,
                    "type": "STRING",
                    "value": "ModiJi"
                },
                "Global_FeedbackSurveyOptIn": {
                    "agentEditable": true,
                    "agentViewable": true,
                    "displayName": "Post Call Survey Opt-in",
                    "global": true,
                    "isSecure": false,
                    "name": "Global_FeedbackSurveyOptIn",
                    "reportable": true,
                    "secureKeyId": "",
                    "secureKeyVersion": 0,
                    "type": "STRING",
                    "value": "uninitialized"
                },
                "dn": {
                    "agentEditable": false,
                    "agentViewable": true,
                    "displayName": "dn",
                    "global": false,
                    "isSecure": false,
                    "name": "dn",
                    "reportable": false,
                    "secureKeyId": "",
                    "secureKeyVersion": 0,
                    "type": "STRING",
                    "value": "+15109024297"
                },
                "virtualTeamName": {
                    "agentEditable": false,
                    "agentViewable": true,
                    "displayName": "virtualTeamName",
                    "global": false,
                    "isSecure": false,
                    "name": "virtualTeamName",
                    "reportable": false,
                    "secureKeyId": "",
                    "secureKeyVersion": 0,
                    "type": "STRING",
                    "value": "Queue_MCM"
                }
            },
            "callAssociatedDetails": {
                "ani": "9487554325",
                "dn": "+15109024297",
                "ronaTimeout": "25",
                "virtualTeamName": "Queue_MCM"
            },
            "callFlowParams": {},
            "callProcessingDetails": {
                "EP_ID": "6941634b-c781-4d0a-8d70-bd2a2174dcd7",
                "QMgrName": "aqm",
                "QueueId": "0025a125-4d2c-4e1a-833d-909e95a389cc",
                "ROUTING_TYPE": "queueBasedRouting",
                "ani": "9487554325",
                "checkAgentAvailability": "false",
                "contactAssignmentType": "ACD",
                "customerRegion": "intgus1",
                "dnis": "+15109024297",
                "fcDesktopView": "eNp9kE0LgzAMhv9LzgpzHxev206DXeZtDIk2h0JsXa3CEP/7Oiaj2tFLDnmfJOQZodVtqgcykN9HUNgQ5IBKQgIDGokV042erreBKfkBQgV55ueDNLZHLgib66ezhrc+XFBnL/QKoJ0PWQeVy5IFE/v12rOQAq3LA/QA0yMBqSwZrK3UKm1REfsWOqp7Q2WlNcdtzKCgWjbIcTMz6w7HpSgi/rJxL/EvF0KOyHxC+9/F9AYS3a1l",
                "fceRegisteredEvents": "ContactLastAgentRemoved",
                "flowTagId": "Latest",
                "mohFileName": "defaultmusic_on_hold.wav",
                "participantInviteTimeout": "false",
                "priority": "10",
                "queuedDestinationID": "0025a125-4d2c-4e1a-833d-909e95a389cc",
                "queuedTo": "Queue",
                "ronaTimeout": "25",
                "taskToBeSelfServiced": "false",
                "tenantId": "58f1a59e-245c-4536-9ee4-06560658e493",
                "virtualTeamName": "Queue_MCM",
                "vteamId": "0025a125-4d2c-4e1a-833d-909e95a389cc",
                "workflowId": "62a165a995fe092e845f4804",
                "workflowName": "FlowSameer"
            },
            "contactDirection": {
                "type": "INBOUND"
            },
            "createdTimestamp": 1758824102098,
            "currentVTeam": "0025a125-4d2c-4e1a-833d-909e95a389cc",
            "flowProperties": null,
            "interactionId": "3bfe5b7b-3c99-40f5-9d30-08c81060b3a8",
            "isFcManaged": true,
            "isMediaForked": false,
            "isTerminated": false,
            "mainInteractionId": "3bfe5b7b-3c99-40f5-9d30-08c81060b3a8",
            "media": {
                "3bfe5b7b-3c99-40f5-9d30-08c81060b3a8": {
                    "holdTimestamp": null,
                    "isHold": false,
                    "mType": "mainCall",
                    "mediaMgr": "callmm",
                    "mediaResourceId": "3bfe5b7b-3c99-40f5-9d30-08c81060b3a8",
                    "mediaType": "telephony",
                    "participants": [
                        "9487554325"
                    ]
                }
            },
            "mediaChannel": "telnyx",
            "mediaProperties": null,
            "mediaType": "telephony",
            "orgId": "58f1a59e-245c-4536-9ee4-06560658e493",
            "outboundType": null,
            "owner": null,
            "parentInteractionId": "3bfe5b7b-3c99-40f5-9d30-08c81060b3a8",
            "participants": {
                "9487554325": {
                    "callerId": null,
                    "hasJoined": true,
                    "hasLeft": false,
                    "id": "9487554325",
                    "isInPredial": false,
                    "pType": "Customer",
                    "type": "Customer"
                }
            },
            "previousVTeams": [
                "6941634b-c781-4d0a-8d70-bd2a2174dcd7"
            ],
            "queuedTimestamp": 1758824103297,
            "state": "new",
            "workflowManager": null
        },
        "interactionId": "3bfe5b7b-3c99-40f5-9d30-08c81060b3a8",
        "mediaResourceId": "3bfe5b7b-3c99-40f5-9d30-08c81060b3a8",
        "orgId": "58f1a59e-245c-4536-9ee4-06560658e493",
        "queueMgr": "aqm",
        "reason": "USER_DECLINED",
        "reasonCode": 156,
        "trackingId": "e544a8e5-2c4f-4a1d-8fb2-66fe3443883f",
        "type": "AgentContactAssignFailed"
    },
    "orgId": "58f1a59e-245c-4536-9ee4-06560658e493",
    "trackingId": "notifs_9cc2b4a2-6f87-487b-9e03-f2686b1eb17e",
    "type": "RoutingMessage"
}
```
