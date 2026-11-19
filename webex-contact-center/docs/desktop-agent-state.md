---
type: Guide
title: Agent State and Availability
display_title: Agent State and Availability
canonical_url: https://developer.webex.com/docs/desktop-agent-state
content_type: documentation
product_group:
- webex-contact-center
categories:
- webex-contact-center
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/desktop-agent-state)

Read agent information and manage availability by media channel with the Desktop SDK.

## Before You Begin

Install and initialize the SDK as described in [Get Started with the Desktop SDK](https://developer.webex.com/docs/desktop-sdk-getting-started). Your widget must run inside Webex Contact Center Desktop.

## Desktop Actions

Auxiliary-code pagination uses `Desktop.agentConfigJsApi`. The other methods in this section use `Desktop.actions`.

### fetchPaginatedAuxCodes

- Retrieves the current idle codes or the current wrap up codes. 
- Example for idle codes: `Idle`, `Coffee break`, `Meeting`, `Tea`.
- Example for wrapup codes: `Credit Card Issue`, `Medical Query`, `Sales Explained`.

**Example**
Fetch Idle codes : 

```javascript
const idleCodes = await Desktop.agentConfigJsApi.fetchPaginatedAuxCodes(
  {
    workType:"IDLE_CODE", // or "WRAP_UP_CODE"
    page: 0,
    pageSize: 100,
    search: "",
    customFilter: ""
  }
);// => Get page 0 of 100 idleCodes from Desktop
```

**Parameters**

| Name      | Type   | Description                                                                                                                                                                        | Required |
| --------- | ------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- |
| workType | String | Specifies the required auxillary code is a wrapup code or an idle code.                                                                                                                                             | Yes      |
| page | number | Fetch details for the particular page number.                                                                                                                                            | No      |
| pageSize | number | Fetch the total number of items presant in one page.                                                                                                                                            | No      |
| search | String | Pass the search parameter.                                                                                                                                            | No      |
| customFilter | String | String that contains conditions for further filtering the results. This is based on the [rsql syntax](https://github.com/perplexhub/rsql-jpa-specification#rsql-syntax-reference).                                                                                                                                            | No      |

**Returns**
```json
{
    "meta": {
        "orgid": "58f1a59e-245c-4536-9ee4-06560658e493",
        "page": 0,
        "pageSize": 100,
        "totalPages": 10,
        "totalRecords": 910,
        "links": {
            "next": "/organization/58f1a59e-245c-4536-9ee4-06560658e493/v2/auxiliary-code?filter=active%3D%3Dtrue;workTypeCode%3D%3DIDLE_CODE&attributes=id,isSystemCode,name,defaultCode&desktopProfileFilter=true&page=1&pageSize=100&sort=name,asc",
            "last": "/organization/58f1a59e-245c-4536-9ee4-06560658e493/v2/auxiliary-code?filter=active%3D%3Dtrue;workTypeCode%3D%3DIDLE_CODE&attributes=id,isSystemCode,name,defaultCode&desktopProfileFilter=true&page=9&pageSize=100&sort=name,asc",
            "self": "/organization/58f1a59e-245c-4536-9ee4-06560658e493/v2/auxiliary-code?filter=active==true;workTypeCode==IDLE_CODE&attributes=id,isSystemCode,name,defaultCode&page=0&pageSize=100&desktopProfileFilter=true&sort=name,ASC",
            "first": "/organization/58f1a59e-245c-4536-9ee4-06560658e493/v2/auxiliary-code?filter=active%3D%3Dtrue;workTypeCode%3D%3DIDLE_CODE&attributes=id,isSystemCode,name,defaultCode&desktopProfileFilter=true&page=0&pageSize=100&sort=name,asc"
        }
    },
    "data": [
        {
            "isSystem": false,
            "name": "A_idleTest",
            "id": "6d686095-80df-4286-8b41-0a937990c905",
            "isDefault": true
        },
        {
            "isSystem": false,
            "name": "Break",
            "id": "3c5fa5f2-21fe-41cb-a5a3-5d71eccd5e1a",
            "isDefault": false
        }
    ]
}
```
Fetch wrap up codes :
```javascript
const wrapUpCodes = await Desktop.agentConfigJsApi.fetchPaginatedAuxCodes(
  {
    workType:"WRAP_UP_CODE",
    page: 0,
    pageSize: 100,
    search: "",
    customFilter: ""
  }
); 
// => Get page 0 of 100 of wrapUpCodes from Desktop
```
**Returns**
```json
{
    "meta": {
        "orgid": "58f1a59e-245c-4536-9ee4-06560658e493",
        "page": 0,
        "pageSize": 100,
        "totalPages": 3,
        "totalRecords": 211,
        "links": {
            "next": "/organization/58f1a59e-245c-4536-9ee4-06560658e493/v2/auxiliary-code?filter=active%3D%3Dtrue;workTypeCode%3D%3DWRAP_UP_CODE&attributes=id,isSystemCode,name,defaultCode&desktopProfileFilter=true&page=1&pageSize=100&sort=name,asc",
            "last": "/organization/58f1a59e-245c-4536-9ee4-06560658e493/v2/auxiliary-code?filter=active%3D%3Dtrue;workTypeCode%3D%3DWRAP_UP_CODE&attributes=id,isSystemCode,name,defaultCode&desktopProfileFilter=true&page=2&pageSize=100&sort=name,asc",
            "self": "/organization/58f1a59e-245c-4536-9ee4-06560658e493/v2/auxiliary-code?filter=active==true;workTypeCode==WRAP_UP_CODE&attributes=id,isSystemCode,name,defaultCode&page=0&pageSize=100&desktopProfileFilter=true&sort=name,ASC",
            "first": "/organization/58f1a59e-245c-4536-9ee4-06560658e493/v2/auxiliary-code?filter=active%3D%3Dtrue;workTypeCode%3D%3DWRAP_UP_CODE&attributes=id,isSystemCode,name,defaultCode&desktopProfileFilter=true&page=0&pageSize=100&sort=name,asc"
        }
    },
    "data": [
        {
            "isSystem": false,
            "name": "Break",
            "id": "fc4cae32-0b5f-4409-ad19-7ff570f68f20",
            "isDefault": false
        },
        {
            "isSystem": false,
            "name": "Customer Disconnected",
            "id": "cd0110c9-3fb5-4cf8-937f-e8fa55d46d01",
            "isDefault": true
        }
    ]
}
```

### getIdleCodes()

**Deprecated since January 16, 2025:** Use [fetchPaginatedAuxCodes](https://developer.webex.com/docs/desktop-agent-state#fetchpaginatedauxcodes) to retrieve auxiliary codes.

Retrieves the current idle codes. Example: Idle, Coffee break, Meeting, Tea.

**Example**

```javascript
const idleCodes = await Desktop.actions.getIdleCodes();
// => Get current idleCodes from Desktop store
```

**Returns**
`{Array}` The array of objects.

**Example Response**

```javascript
const codes = [
{
    id: "1643",
    isDefault: false,
    isSystem: true,
    name: "RONA"
}, {
    id: "1644",
    isDefault: true,
    isSystem: false,
    name: "Meeting"
}
];
```

### getWrapUpCodes()

**Deprecated since January 16, 2025:** Use [fetchPaginatedAuxCodes](https://developer.webex.com/docs/desktop-agent-state#fetchpaginatedauxcodes) to retrieve auxiliary codes.

Retrieves the wrap up codes. Example: Credit Card Issue, Medical Query, Sales Explained.

**Example**

```javascript
const wrapUpCodes = await Desktop.actions.getWrapUpCodes()
// => Get current wrapUpCodes from Desktop store
// Retrieves configured wrap-up codes, such as "Credit Card Issue" or "Medical Query".
```

**Returns**

`{Array}` The array of objects.

**Example Response**

```javascript
const codes = [
{
    id: "2063",
    isDefault: false,
    isSystem: false,
    name: "Account Information Explained"
}, {
    id: "2061",
    isDefault: false,
    isSystem: false,
    name: "Credit Card Issue"
}
];
```

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

## Agent State Information Module

The `Desktop.agentStateInfo` module listens for the latest data updates of agent related information.

**Example**

```typescript
import { Service } from "@wxcc-desktop/sdk-types";

type IdleCodeData = { id: string; name: string };

type LatestInfoData = {
  agentName?: string,
  agentProfileID?: string,
  agentSessionId?: string,
  teamId?: string,
  teamName?: string,
  dn?: string,
  status?: string,
  /** @deprecated Global status; not valid with granular state control. Consume agent state from channelsStatesMap instead. */
  subStatus?: string,
  /** Per-channel agent state (agentState, stateChangeTimestamp, etc.). Keyed by channel type (e.g. telephony, chat). With granular state control, consume agent state from this instead of subStatus. */
  channelsStatesMap?: Record<string, { agentState?: string; stateChangeTimestamp?: number; pendingIdle?: boolean; auxCodeId?: string; availableChannelCount?: number | null; totalChannelCount?: number | null; stateChangeReason?: string; lastIdleCodeChangeTimestamp?: number | null; [key: string]: unknown }>,
  idleCodes?: Service.Aqm.Configs.Entity[],
  idleCode?: IdleCodeData,
  wrapupCodes?: Service.Aqm.Configs.Entity[],
  outDialRegex?: string,
  isOutboundEnabledForTenant?: boolean,
  isOutboundEnabledForAgent?: boolean,
  isAdhocDialingEnabled?: boolean,
  isAgentAvailableAfterOutdial?: boolean,
  isEndCallEnabled?: boolean,
  isEndConsultEnabled?: boolean,
  allowConsultToQueue?: boolean,
  isCampaignManagementEnabled?: boolean,
  agentPersonalStatsEnabled?: boolean
};
```

These fields may be unavailable until the module loads or when the corresponding feature is disabled. Guard optional fields before reading them. Nested idle-code fields apply when `idleCode` is present.

The following table lists the payload details:

| Name                         | Type    | Description                                                                                                                                                                                                                                                                                                                                                                                                               | Required |
| ---------------------------- | ------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- |
| agentName | String | Agent's name. | No |
| agentProfileID | String | Agent profile identifier. | No |
| agentSessionId | String | Agent session identifier. | No |
| teamId                       | String  | Unique identifier of the team.                                                                                                                                                                                                                                                                                                                                                                                            | No       |
| teamName                     | String  | Name of the team.                                                                                                                                                                                                                                                                                                                                                                                                         | No       |
| dn                           | String  | Dial number (DN) to the entry point.                                                                                                                                                                                                                                                                                                                                                                                      | No       |
| status                       | String  | Agent log in status such as LoggedIn.                                                                                                                                                                                                                                                                                                                                                                                     | No       |
| subStatus                    | String  | **Deprecated.** Global agent availability status (e.g. Available). Not valid with granular state control; consume agent state from **channelsStatesMap** instead.                                                                                                                                                                                          | No       |
| channelsStatesMap            | Object  | Map keyed by channel type (e.g. telephony, chat, email, social). Each value has agentState, stateChangeTimestamp, pendingIdle, auxCodeId, availableChannelCount, totalChannelCount, stateChangeReason, lastIdleCodeChangeTimestamp, and related fields. With granular state control, consume agent state from this map for status and state timestamps per channel.                                                                                                            | No       |
| idleCodes                    | Array   | Indicates the reason that the agent is idle and not available for any routed requests. The agent changes the state from Available to any configured idle codes. Example: Idle, Coffee break, Meeting, Tea.                                                                                                                                                                                                                | No       |
| idleCode                     | Object  | Indicates the current reason that the agent is idle. For example, the agent changed the idle state from Coffee break to Meeting.When the agent is in the Available state, the idleCode is undefined.                                                                                                                                                                                                                      | No       |
| --> id                       | String  | Idle code unique identifier.                                                                                                                                                                                                                                                                                                                                                                                              | Yes      |
| -->name                      | String  | Name of the reason code for the idle state, currently used by the agent. Example: Idle, Coffee break, Meeting, Tea.                                                                                                                                                                                                                                                                                                       | Yes      |
| wrapupCodes                  | Array   | The wrap up reason codes indicating that the agent has ended the interactions with the customer                                                                                                                                                                                                                                                                                                                           | No       |
| outDialRegex                 | String  | Outdial regular expression validity.                                                                                                                                                                                                                                                                                                                                                                                      | No       |
| isOutboundEnabledForTenant   | Boolean | Determines whether the outbound feature is enabled for the tenant.<br>- True—Enables the outbound feature for the tenant.<br>- False—Disables the outbound feature for the tenant.                                                                                                                                                                                                                                        | No       |
| isOutboundEnabledForAgent    | Boolean | Determines whether the outbound feature is enabled for the agent.<br>- True—Enables the outbound feature for the agent.<br>- False—Disables the outbound feature for the agent.                                                                                                                                                                                                                                           | No       |
| isAdhocDialingEnabled        | Boolean | Determines whether an agent can use a phone number that is not stated in the enterprise address book to make an outdial call.<br>- True—An agent is allowed to use phone numbers (using the **Dialpad**) that are not stated in the enterprise address book to make an outdial call.<br>- False—An agent is allowed to use only the phone numbers that are stated in the enterprise address book to make an outdial call. | No       |
| isAgentAvailableAfterOutdial | Boolean | Determines whether an agent is available or not after the outdial call ends.<br>- True—The agent is available after the outdial call ends, and the agent state is set as Available.<br>- False—The agent is not available after the outdial call ends, and the agent state is set as Idle.                                                                                                                                | No       |
| isEndCallEnabled             | Boolean | Determines whether an agent can end a voice call or not.<br>- True—Enables an agent to end a voice call.<br>- False—Disables an agent to end a voice call, and the agent must ask the customer to end the voice call.                                                                                                                                                                                                     | No       |
| isEndConsultEnabled          | Boolean | Determines whether an agent can end a consult call or not. The default value is true.<br>- True—Enables an agent to end a consult call.<br>- False—Disables an agent to end a consult call.                                                                                                                                                                                                                               | No       |
| allowConsultToQueue          | Boolean | Determines whether to consult an active call to a queue.<br>- True—Enables the consult call to a queue.<br>- False—Disables the consult call to a queue.                                                                                                                                                                                                                                                                  | No       |
| isCampaignManagementEnabled  | Boolean | Determines whether the outbound campaign call feature is enabled or not.<br>- True—Enables the outbound campaign call feature for an agent.<br>- False—Disables the outbound campaign call feature for an agent.                                                                                                                                                                                                          | No       |
| agentPersonalStatsEnabled    | Boolean | Determines whether the Agent Performance Statistics (APS) reports page is enabled or not.<br>- True—Enables the Agent Performance Statistics (APS) reports page for an agent.<br>- False—Disables the Agent Performance Statistics (APS) reports page for an agent.                                                                                                                                                       | No       |

### Methods

#### latestData

Fetches the latest user related information.
Access `latestData` inside the `updated` event hander (See [Events](https://developer.webex.com/docs/desktop-agent-state#events) section). This will make sure that `agentstateinfo` module is loaded before accessing the property.


**Example**

```typescript
const onUpdated = () => {
  const latestData: LatestInfoData = Desktop.agentStateInfo.latestData;
  console.log(latestData);
};
Desktop.agentStateInfo.addEventListener("updated", onUpdated);

// Call this function during widget teardown.
function cleanupAgentStateListener() {
  Desktop.agentStateInfo.removeEventListener("updated", onUpdated);
}
```

**Returns**
`{Object}` Lists the latest user related information.

**Example Response**

```json
{
    "agentName": "John Doe",
    "teamName": "Sales",
    "teamId": "964",
    "dn": "8895579172",
    "status": "LoggedIn",
    "subStatus": "Idle",
    "idleCodes": [{
        "id": "1646",
        "isDefault": false,
        "isSystem": true,
        "name": "Aux on Login"
    }],
    "wrapupCodes": [{
        "id": "2065",
        "isDefault": false,
        "isSystem": false,
        "name": "Wrapping up as customer disconnected"
    }],
    "outDialRegex": "([0-9a-zA-Z]+[-._])*[0-9a-zA-Z]+",
    "isOutboundEnabledForTenant": true,
    "isOutboundEnabledForAgent": true,
    "isAdhocDialingEnabled": true,
    "isAgentAvailableAfterOutdial": true,
    "isEndCallEnabled": true,
    "isEndConsultEnabled": true,
    "allowConsultToQueue": true,
    "isCampaignManagementEnabled": true,
    "agentPersonalStatsEnabled": true
}
```

#### stateChange(state, auxCodeIdArray)

**Deprecated:** Use [stateChangeV2()](https://developer.webex.com/docs/desktop-agent-state#statechangev2channeltype-state-auxcodeid-reason-agentid) for channel-specific state changes. The [Contact Center changelog](https://developer.webex.com/docs/api/changelog/webex-contact-center) announces deprecation beginning in March 2026.

Changes the state of an agent. For example from Available to Idle.

**Example**

```javascript
await Desktop.agentStateInfo.stateChange({
  state: "Available",
  auxCodeIdArray: "0"
});

// An example for Idle with an Idle Code

await Desktop.agentStateInfo.stateChange({
  state: "Meeting",
  auxCodeIdArray: "3bdbf3f3-0232-4ae3-b26c-16437c18a13d"
});
```

**Parameters**

| Name           | Type   | Description                           | Required |
| -------------- | ------ | ------------------------------------- | -------- |
| state          | String | Current agent state.                  | Yes      |
| auxCodeIdArray | String | Unique identifier of the agent state. | Yes      |

**Returns**

`{Object}` Lists the agent state change information.

**Example Response**

```json
{
    "data": {
        "agentId": "7c867aa9-ec768-341a-b767-e5hd6ae7g701",
        "agentSessionId": "3d017488-527a-4e89-9313-5d4eb353c789",
        "auxCodeId": "0",
        "connectedChannels": [
            "38136791-cf79-4663-a5d0-39b0d094abf8"
        ],
        "eventType": "AgentDesktopMessage",
        "lastIdleCodeChangeTimestamp": null,
        "lastStateChangeReason": "",
        "lastStateChangeTimestamp": 1612245463183,
        "orgId": "f111e3af-1a45-42ef-9erf-4562354b8a25",
        "status": "LoggedIn",
        "subStatus": "Available",
        "trackingId": "9008a4a0-651b-11eb-a97d-0d76c582d799",
        "type": "AgentStateChangeSuccess"
    },
    "orgId": "f111e3af-1a45-42ef-9erf-4562354b8a25",
    "trackingId": "notifs_aa848b62-4fcf-4d4c-95ad-1233bb7f899c",
    "type": "AgentStateChange"
}
```
#### stateChangeV2(channelType, state, auxCodeId, reason, agentId)

Changes the state of a particular channel for the agent. For example from Available to Idle for "Chat" channel.
**Note**: For one channelType, all the channels must have same state. For example: 5 channels for type "Chat" will always have same state, while "Telephony" can have different state than "Chat".

**Example**

```javascript
await Desktop.agentStateInfo.stateChangeV2({
  channelType: ["telephony", "chat"],
  state: "Available",
  auxCodeId: "0",
  reason: "Available",
  agentId: "1a80ba23-194b-49af-9b93-074b3ecc852a",
});

// An example for Idle with an Idle Code

await Desktop.agentStateInfo.stateChangeV2({
  channelType: ["telephony"],
  state: "Idle",
  auxCodeId: "3bdbf3f3-0232-4ae3-b26c-16437c18a13d",
  reason: "Lunch",
  agentId: "1a80ba23-194b-49af-9b93-074b3ecc852a",
});
```

**Parameters**

| Name           | Type     | Description                                             | Required |
| -------------- | -------- | ------------------------------------------------------- | -------- |
| channelType    | String[] | Channel types for which the state needs to be applied.  | Yes      |
| state          | String   | Agent state to be applied.                              | Yes      |
| auxCodeId      | String   | Unique identifier of the agent state.                   | Yes      |
| reason         | String   | Reason for changing the state.                          | NO       |
| agentId        | String   | Unique identifier for the agent whose state is changed. | Yes      |

**Returns**

Multiple `{Object}` Lists the agent state change information per channel. The number of responses is equal to the number of channels mentioned in the channelType array.

**Timestamp units:** The `agentChannelStateDetail` fields in SDK response and event payloads use epoch milliseconds, as defined by the Contact Control API contract. This differs from the `STORE.agent.channelsStatesMap` fields documented in [Widget Data and Desktop Layout](https://developer.webex.com/docs/desktop-widget-data-layout#storeagent-agent-profile-attributes), which use epoch seconds. Use the units for the source you consume; a seconds value needs multiplication by 1,000 before passing it to `new Date()`.
NOTE: The responses are separate. NOT a single array of objects.

**Example Response**

```json
{
  "data": {
    "agentId": "1a80ba23-194b-49af-9b93-074b3ecc852a",
    "channelType": "telephony",
    "agentChannelStateDetail": {
      "agentState": "Available",
      "pendingIdle": false,
      "auxCodeId": "0",
      "availableChannelCount": 1,
      "manuallyAssignedChannelCount": null,
      "manuallyAssignedAvailableChannelCount": null,
      "totalManuallyAssignedChannelCount": null,
      "totalChannelCount": 1,
      "stateChangeTimestamp": 1757579405000,
      "stateChangeReason": "Available",
      "lastIdleCodeChangeTimestamp": 1757578805000
    },
    "changedBy": null,
    "changedById": null,
    "changedByName": null,
    "connectedChannels": ["38136791-cf79-4663-a5d0-39b0d094abf8"],
    "agentSessionId": "3d017488-527a-4e89-9313-5d4eb353c789",
    "type": "AgentChannelStateChanged"
  },
  "orgId": "b33fb142-4d65-4781-9899-19b0363cd45f",
  "trackingId": "notifs_aa848b62-4fcf-4d4c-95ad-1233bb7f899c",
  "type": "AgentDesktopMessage"
}
```
```json
{
  "data": {
    "agentId": "1a80ba23-194b-49af-9b93-074b3ecc852a",
    "channelType": "chat",
    "agentChannelStateDetail": {
      "agentState": "Available",
      "pendingIdle": false,
      "auxCodeId": "0",
      "availableChannelCount": 1,
      "manuallyAssignedChannelCount": null,
      "manuallyAssignedAvailableChannelCount": null,
      "totalManuallyAssignedChannelCount": null,
      "totalChannelCount": 2,
      "stateChangeTimestamp": 1757579405000,
      "stateChangeReason": "Available",
      "lastIdleCodeChangeTimestamp": null
    },
    "changedBy": null,
    "changedById": null,
    "changedByName": null,
    "connectedChannels": ["38136791-cf79-4663-a5d0-39b0d094abf8", "4a235679-de68-5774-b651-nm76d094dj67"],
    "agentSessionId": "3d017488-527a-4e89-9313-5d4eb353c789",
    "type": "AgentChannelStateChanged"
  },
  "orgId": "b33fb142-4d65-4781-9899-19b0363cd45f",
  "trackingId": "notifs_aa848b62-4fcf-4d4c-95ad-1233bb7f899c",
  "type": "AgentDesktopMessage"
}
```

### Events

#### addEventListener

Listens to an event named **updated** that is logged if the dn, status, or subStatus field is changed.

**Deprecation:** The **subStatus** field (global status) in the **updated** event is not valid with granular state control. Consume agent state from **STORE.agent.channelsStatesMap** and use the **eAgentChannelStateChanged** event for state changes and **stateChangeTimestamp** per channel.

For more information, see [addEventListener(event, handler)](https://developer.webex.com/docs/desktop-contact-events#addeventlistenerevent-handler).

**Example**

```javascript
Desktop.agentStateInfo.addEventListener("updated", updatedList => {
  console.log(updatedList);
});
```

**Example event payload**

```json
[
  {
    "name": "dn",
    "value": "+12580258011",
    "oldValue": ""
  },
  {
    "name": "status",
    "value": "LoggedIn",
    "oldValue": "DefaultState"
  },
  {
    "name": "subStatus",
    "value": "Available",
    "oldValue": ""
  }
]
```
**NOTE**: While using stateChangeV2 api, the listener needs to be changed from "updated" to "eAgentChannelStateChanged". This is a breaking change, and will NOT work with "updated".

**Example**

```javascript
Desktop.agentStateInfo.addEventListener("eAgentChannelStateChanged", eventData => console.log(eventData));

```

**Example event payload**

```javascript
const channelStateEvent = {
  agentId: "1a80ba23-194b-49af-9b93-074b3ecc852a",
  orgId: "b33fb142-4d65-4781-9899-19b0363cd45f",
  channelType: "telephony",
  agentChannelStateDetail: {
    agentState: "Available",
    pendingIdle: false,
    auxCodeId: "0",
    availableChannelCount: 1,
    manuallyAssignedChannelCount: null,
    manuallyAssignedAvailableChannelCount: null,
    totalManuallyAssignedChannelCount: null,
    totalChannelCount: 4,
    stateChangeTimestamp: 1757579405000,
    stateChangeReason: "Available",
    lastIdleCodeChangeTimestamp: 1757578805000
  },
  changedBy: null,
  changedById: null,
  changedByName: null,
  connectedChannels: ["38136791-cf79-4663-a5d0-39b0d094abf8"],
  agentSessionId: "3d017488-527a-4e89-9313-5d4eb353c789",
  trackingId: "9008a4a0-651b-11eb-a97d-0d76c582d799",
  type: "AgentChannelStateChanged",
  eventType: "AgentDesktopMessage"
}
```

## Verify Channel State Changes

When using `stateChangeV2`, listen for `eAgentChannelStateChanged` and read the corresponding entry in `STORE.agent.channelsStatesMap`. The `updated` event does not report the granular state changes. See [Widget Data and Desktop Layout](https://developer.webex.com/docs/desktop-widget-data-layout).

## Related Pages

- [Agent Desktop overview](https://developer.webex.com/docs/desktop)
- [Desktop SDK Reference](https://developer.webex.com/docs/desktop-sdk-reference)
