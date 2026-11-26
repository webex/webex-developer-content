---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-call-control
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Desktop Actions
- addCustomTask()
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

### addCustomTask()

Adds a new custom task within your widget. The task appears in the Desktop task list.

**Note:** To keep the list of tasks up to date within your widget, you must add event listeners and subscribe to asynchronous events. The events signify new tasks being assigned to an agent. For more information, see [Asynchronous Events](https://developer.webex.com/docs/desktop-contact-events#asynchronous-events).

**Example**

```javascript
const contactPayload = {
        mediaResourceId: "49bcf26b-ec75-4351-89fa-55d54682c20c",
        eventType: "RoutingMessage",
        agentId: "16839506-7c48-4a71-ba1b-d585e5d37607",
        trackingId: "354deeae-c98a-4a8c-9e04-e56e129fdb9f",
        interaction: {
            isFcManaged: false,
            isTerminated: false,
            mediaType: "telephony",
            previousVTeams: ["AXCZ0YCAXrf9I0XFBI7b"],
            state: "connected",
            currentVTeam: "3268",
            participants: {
                "+19997770096": {
                    id: "+19997770096",
                    pType: "Customer",
                    type: "Customer"
                },
                "aad323de-32d8-48c9-af6b-b68dfbabfe20": {
                    name: "uuip-agent2",
                    pType: "Agent",
                    teamName: "Team X",
                    lastUpdated: 1597681728863,
                    teamId: "962",
                    joinTimestamp: 1597681728863,
                    isConsulted: false,
                    hasJoined: true,
                    consultTimestamp: null,
                    dn: "9997770194",
                    queueId: "3268",
                    id: "16839506-7c48-4a71-ba1b-d585e5d37607",
                    sessionId: "319d8e83-2a75-4ef3-9cb8-1c845edb15a0",
                    consultState: null,
                    queueMgrId: "aqm",
                    siteId: "473",
                    type: "Agent",
                    channelId: "ab8b3603-84a7-4f61-b987-9044b4d69cf2",
                    wrapUpTimestamp: null,
                    isWrapUp: false
                }
            },
            interactionId: "49bcf26b-ec75-4351-89fa-55d54682c20c",
            orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
            callAssociatedData: {
                customerName: {
                    value: "test",
                    name: "r",
                    agentEditable: false,
                    type: "s",
                    displayName: "d"
                }
            },
            callAssociatedDetails: {
                virtualTeamName: "Queue - Telephony",
                ani: "+19997770096",
                ronaTimeout: "30",
                dn: "+12147659000",
                pathId: " StartCall PlayDone out out out",
                IvrPath: " EOI",
                subject: "",
                toAddress: "",
                inReplyTo: "",
                customerName: "",
                ccAddress: "",
                entryPointId: "",
                accountId: "",
                reasonCode: "",
                reason: "",
                references: "",
                contentType: "",
                date: "",
                replyToAddress: "",
                fromAddress: "",
                messageId: "",
                from: "",
                threadId: "",
                bccAddress: "",
                queueType: "",
                dnis: "",
                category: "",
                sourceNumber: "",
                sourcePage: "",
                appUser: "",
                customerNumber: ""
            },
            callProcessingDetails: {
                QMgrName: "aqm",
                pauseResumeEnabled: "true",
                taskToBeSelfServiced: "false",
                ani: "+19997770096",
                recordInProgress: "true",
                pauseDuration: "10",
                dnis: "+12147659000",
                tenantId: "133",
                QueueId: "3268",
                vteamId: "3268",
                jscriptId: "AXCZ4c3mjkwgAuS7vSIU",
                customerName: "",
                virtualTeamName: "Queue - Telephony",
                ronaTimeout: "30",
                category: "",
                reason: "",
                sourceNumber: "",
                sourcePage: "",
                appUser: "",
                customerNumber: "",
                reasonCode: "",
                IvrPath: " EOI",
                pathId: " StartCall PlayDone out out out",
                fromAddress: ""
            },
            media: {
                "49bcf26b-ec75-4351-89fa-55d54682c20c": {
                    mediaResourceId: "49bcf26b-ec75-4351-89fa-55d54682c20c",
                    mediaType: "telephony",
                    mediaMgr: "vmm",
                    participants: ["+19997770096", "16839506-7c48-4a71-ba1b-d585e5d37607"],
                    mType: "mainCall",
                    isHold: false,
                    holdTimestamp: null
                }
            },
            owner: "16839506-7c48-4a71-ba1b-d585e5d37607",
            mediaChannel: "broadcloud",
            contactDirection: {
                type: "INBOUND"
            },
            callFlowParams: {
                Play2: {
                    name: "Play2",
                    qualifier: "",
                    description: "(A valid text.)",
                    valueDataType: "string",
                    value: "Welcome to Agent Team Space"
                },
                Queue3: {
                    name: "Queue3",
                    qualifier: "vteam",
                    description: "(vteam, A valid VTeam.)",
                    valueDataType: "string",
                    value: "3268"
                }
            }
        },
        interactionId: "49bcf26b-ec75-4351-89fa-55d54682c20c",
        orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
        queueMgr: "aqm",
        type: "AgentContactAssigned",
        destAgentId: "16839506-7c48-4a71-ba1b-d585e5d37607",
        consultMediaResourceId: "",
        owner: "",
        isConferencing: false
};
Desktop.actions.addCustomTask(contactPayload);
// => Add custom task object in Desktop store
```
