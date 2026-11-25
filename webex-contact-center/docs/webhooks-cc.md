---
type: Guide
title: Contact Center Webhooks | Event reference
display_title: Event reference
canonical_url: https://developer.webex.com/docs/webhooks-cc
content_type: documentation
product_group:
- webex-contact-center
categories:
- create
- webex-contact-center
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/webhooks-cc)

Find Webex Contact Center webhook event types, resource versions, and event-specific payload fields.

---

<a id="using-webhooks"></a>

<a id="overview"></a>

## Use this reference

This catalog covers Contact Center agent, capture, task, and flow events. See [registration](https://developer.webex.com/docs/using-webhooks#customer-onboarding-page) for subscriptions and [receiving events](https://developer.webex.com/docs/receive-and-verify-contact-center-webhooks) for the envelope and signatures. Messaging, Meetings, Calling, and platform events have a [separate reference](https://developer.webex.com/docs/webhook-event-reference).

Each resource table lists the resource, event, trigger, and resource versions. Select an event to find its `data` fields, types, and examples. Copy event identifiers, field names, and resource versions exactly as shown.

<a id="use-cases"></a>
<a id="design-considerations"></a>

For use cases, delivery guarantees, reconciliation, ordering, and deduplication, see [delivery, ordering, and reconciliation](https://developer.webex.com/docs/receive-and-verify-contact-center-webhooks#delivery-ordering-and-reconciliation).

## Agents

The agent resource encapsulates the entities which handle the tasks through interactions with customers. An agent can be either a human or bot, and can be either the entity directly handling the task, or an assisting entity i.e. a supervisor. Agents are summarized by the groups they belong to (organization and team), details for the tasks they handle, and their overall availability. For recovery queries, consult [Get Agent Activities](https://developer.webex.com/docs/api/v1/agents/get-agent-activities) for supported query windows.

| Resource | Event | Trigger | Resource version |
| --- | --- | --- | --- |
| `agent` | [`agent:login`](#agent-login) | An Agent has logged in. | `agent:1.0.0`, `agent:2.0.0` |
| `agent` | [`agent:logout`](#agent-logout) | An Agent has logged out. | `agent:1.0.0`, `agent:2.0.0` |
| `agent` | [`agent:state_change`](#agent-state-change) | An Agent’s state has changed. | `agent:1.0.0` |
| `agent` | [`agent:channel_state_change`](#agent-channel-state-change) | An agent's state changed at the channel level. | `agent:2.0.0` |
| `agent` | [`agent:channelType_state_change`](#agent-channeltype-state-change) | An agent's state changed for a specific channel type. | `agent:2.0.0` |

<a id="agent-login"></a>

### Agent Login

`agent:login`

**Resource Version: agent:1.0.0, agent:2.0.0**

An event indicating that an Agent has logged in.

| Field | Type | Description | Example |
| --- | --- | --- | --- |
| `agentId` | `string` | The ID associated with the agent who logged in. | `"8e18afd-db79-449b-b4f5-ae4f1d49f45e"` |
| `destination` | `string` | The phone number that is associated with the agent. | `"31476521"` |
| `profileType` | `string` | The multimedia profile type of the agent. Can be Blended, Blended Real-time, or Exclusive. | `"BLENDED"` |
| `idleCodeId` | `string` | The idle code of the agent when logged in. | `"5"` |
| `currentState` | `string` | The current state that the agent is in. | `"Idle"` |
| `createdTime` | `integer` | The time that the login event occurred in epoch milliseconds. | `160269666391` |
| `teamId` | `string` | The ID associated with an agent’s team. | `"3ce57020-dfd7-47fd-91a1-2783bf4a08e5"` |

<a id="agent-logout"></a>

### Agent Logout

`agent:logout`

**Resource Version: agent:1.0.0, agent:2.0.0**

An event indicating that an Agent has logged out.

| Field | Type | Description | Example |
| --- | --- | --- | --- |
| `agentId` | `string` | The ID associated with the agent who logged out. | `"8e18afd-db79-449b-b4f5-ee4f14d9f45e"` |
| `currentState` | `string` | The current state that the agent is in. | `"logged-out"` |
| `loggedOutBy` | `string` | The mechanism used to log the agent out. | `"SELF"` |
| `createdTime` | `integer` | The time that the logout event occurred in epoch milliseconds. | `160269666391` |

<a id="agent-state-change"></a>

### Agent State Change

`agent:state_change`

**Resource Version: agent:1.0.0**

An event indicating that an Agent’s state has changed.

| Field | Type | Description | Example |
| --- | --- | --- | --- |
| `agentId` | `string` | The ID associated with the agent who is handling the contact. | `"8e18afd-db79-449b-b4f5-ee4f14d9f45e"` |
| `currentState` | `string` | The current state of the agent. Can be idle, available, ringing, not-responding, connected, on-hold, hold-done, consulting, conferencing, consult-done, wrapup, wrapup-done. | `"idle"` |
| `destination` | `string` | The phone number that is associated with the agent. | `"9900163437"` |
| `queueId` | `string` | The ID associated with an agent queue. | `"AXlp8E3f-KJXJ6KOPIK"` |
| `taskId` | `string` | The ID associated with a specific interaction. | `"40fa44a7-b640-4b72-a8cd-5a0502ab2e81"` |
| `createdTime` | `integer` | The time that the state_change event occurred in epoch milliseconds. | `160269666391` |
| `idleCodeId` | `string` | The idle code of the agent when currentState is idle. | `"2651"` |
| `connectedChannels` | `string[]` | List of channels that agent is currently handling. | `["4fae000e-f460-4b5c-8b05-02f7fb5a8061", "4fae000e-fabb-4"]` |
| `wrapUpAuxCodeId` | `string` | The wrapup code the agent selects when ending a task. | `"3183"` |
| `teamId` | `string` | The ID associated with an agent’s team. | `"3ce57020-dfd7-47fd-91a1-2783bf4a08e5"` |

<a id="agent-channel-state-change"></a>

### Agent Channel State Change

`agent:channel_state_change`

**Resource Version: agent:2.0.0**

This event indicates that an agent's state has changed at the channel level. It is available under resource version agent:2.0.0.

| Field | Type | Description | Example |
| --- | --- | --- | --- |
| `agentId` | `string` | The ID associated with the agent who is handling the contact. | `"8e18afd-db79-449b-b4f5-ee4f14d9f45e"` |
| `agentCiUserId` | `string` | The CI user ID associated with the agent. | `"68b1a6bd-1d3e-4cdb-9cb2-1ecd9faaf53d"` |
| `currentState` | `string` | The current state of the agent. Can be idle, available, ringing, not-responding, connected, on-hold, hold-done, consulting, conferencing, consult-done, conference-done, wrapup, wrapup-done. | `"idle"` |
| `channelId` | `string` | The ID of the channel associated with the agent. | `"bc7eedd6-42c6-45c5-9c94-2d34123317e6"` |
| `channelType` | `string` | The type of channel associated with the agent. | `"telephony"` |
| `destination` | `string` | The phone number that is associated with the agent. | `"9900163437"` |
| `queueId` | `string` | The ID associated with an agent queue. | `"AXlp8E3f-KJXJ6KOPIK"` |
| `taskId` | `string` | The ID associated with a specific interaction. | `"40fa44a7-b640-4b72-a8cd-5a0502ab2e81"` |
| `createdTime` | `integer` | The time that the state_change event occurred in epoch milliseconds. | `160269666391` |
| `idleCodeId` | `string` | The idle code of the agent when currentState is idle. | `"2651"` |
| `wrapUpAuxCodeId` | `string` | The wrapup code the agent selects when ending a task. | `"3183"` |
| `teamId` | `string` | The ID associated with an agent's team. | `"3ce57020-dfd7-47fd-91a1-2783bf4a08e5"` |

<a id="agent-channeltype-state-change"></a>

### Agent ChannelType State Change

`agent:channelType_state_change`

**Resource Version: agent:2.0.0**

An event indicating that an Agent's state has changed for a specific channel type. This event is fired when an agent's availability or engagement state transitions within a particular media channel (e.g., telephony, chat, email, or social).

| Field | Type | Description | Example |
| --- | --- | --- | --- |
| `agentId` | `string` | The ID associated with the agent whose channel type state has changed. | `"11bafc46-ae09-4ddf-bf0b-26d24e924f9f"` |
| `agentCiUserId` | `string` | The CI user ID associated with the agent. | `"68b1a6bd-1d3e-4cdb-9cb2-1ecd9faaf53d"` |
| `currentState` | `string` | The current state of the agent for the given channel type. Valid agent states are:<br />**Available** — The agent is available in this channel type and can accept a contact.<br />**Idle** — The agent is currently logged in but not available in this channel type and cannot take contacts. This would be shown on the desktop by the Aux code selected (e.g., lunch).<br />**Engaged** — The agent is actively working on one or more contacts in this channel type.<br />**EngagedOther** — The agent is engaged with a channel type that, due to "Exclusive" or "Blended Realtime" multimedia profile settings, prevents them from accepting a contact in this channel type. For example, if an agent with an Exclusive profile is engaged on an email, they would be "EngagedOther" in Voice, Chat, and Social. Similarly, with a Blended Realtime profile, if the agent is engaged on a Chat contact, they would be "EngagedOther" in the Voice channel type.<br />**WrapUp** — The agent is currently performing wrap-up work on a contact and will transition to Available at conclusion if not working on another contact in that channel type.<br />**Reserved** — The agent has been selected by routing and is in the process of being invited (inbound or outbound). This state is typically short-lived. For cases where a campaign agent is reserved with a reservation call, their state will be Reserved in the voice channel as opposed to Engaged.<br />**LoggedOut** — Although technically not a managed agent state, this indicates the agent is not logged into the system. | `"Available"` |
| `channelType` | `string` | The channel type of the agent for which the state change applies. Can be set to telephony, social, email, or chat. A separate agent:channelType_state_change event is sent per channel type. In the event that the agent is setting more than one channel type state at once, multiple state change events are sent — one per channel type. | `"social"` |
| `pendingIdleState` | `boolean` | Indicates whether the agent has a pending idle state. The value is determined by the following conditions: first, the agent's sub_status must be set to idle (the agent has indicated they want to go idle). If not, pendingIdleState is **false**. Next, the agent's state in the current channel must not yet be idle (e.g., the agent is still Engaged or in WrapUp). If the agent's state in the channel is already idle, pendingIdleState is **false**. Finally, if not all channels in the channelType are idle, then pendingIdleState is **true** — otherwise it is **false**. When **true**, the agent is currently working or wrapping up one or more contacts and will transition to Idle at the conclusion. No further contacts will be given to them in that channel type. On the desktop, the output will reflect the selected Aux code (e.g., "Pending Coffee-Break").<br />Note: In non-voice channels, it is possible to directly set the agent state to Idle although one or more channels are active in a media type. | `false` |
| `idleCodeName` | `string` | The name of the idle (auxiliary) code selected by the agent. This field is populated when the agent's current state is Idle, or when pendingIdleState is true (the agent has selected an idle code but has not yet transitioned). Examples include "Meeting", "Lunch", or "Break". | `"Meeting"` |
| `teamId` | `string` | The ID associated with an agent's team. | `"088ca4da-085c-4563-9b71-d430721f0354"` |
| `createdTime` | `integer` | The time that the channelType_state_change event occurred, in epoch milliseconds. | `1768319367741` |

For agent-specific recovery queries, use [Get Agent Activities](https://developer.webex.com/docs/api/v1/agents/get-agent-activities).

## Captures

The Capture resource is a snippet of media. Specifically, Captures are the recorded pieces of media produced from a Task. Supported channels are Voice, Chat, Email & Social (as applicable for the solution). There can be one or many Captures for any given Task. Captures are accessible for both open (voice only) and closed Tasks (all channels). Requires one of the following scopes cjp:config_read, cjp-analyzer:read.

| Resource | Event | Trigger | Resource version |
| --- | --- | --- | --- |
| `capture` | [`capture:available`](#capture-available) | The recording for a call is available after the call has ended. | `capture:1.0.0` |
| `recording` | [`recording:available`](#recording-available) | A recording is available for an interaction. | `recording:1.0.0` |
| `transcription` | [`transcription:available`](#transcription-available) | A transcript is available for an interaction. | `transcription:1.0.0` |

The existing `capture:available` webhook remains backward-compatible and continues to indicate recording availability. In addition, explicit `recording:available` and `transcription:available` webhook events are available for integrations that want separate recording and transcript readiness signals.

Use these events as follows:

- Subscribe to `capture:available` if your integration already relies on the existing recording-ready webhook behavior.
- Subscribe to `recording:available` if you want an explicit recording-ready signal while preserving the same general payload shape as `capture:available`.
- Subscribe to `transcription:available` if you want an explicit transcript-ready signal.
- Subscribe to more than one of these events if your integration needs both recording and transcript readiness.

When the beta additive events are enabled for your organization for voice interactions:

- `capture:available` and `recording:available` are both delivered for recording readiness
- the two events fan out from the same internal recording-available signal and therefore share the same event `id`
- `capture:available` keeps the existing payload shape
- `recording:available` adds the `contactType` and `channelType` fields

For transcript availability, integrations should use `transcription:available` for both voice and digital interactions. Its payload includes the `contactType` and `channelType` fields. Digital interactions do not emit recording-oriented webhook events for transcript readiness.

<a id="capture-available"></a>

### Capture Available

`capture:available`

**Resource Version: capture:1.0.0**

An event indicating that the recording for a call is available after the call has ended.

| Field | Type | Description | Example |
| --- | --- | --- | --- |
| `taskId` | `string` | The task ID associated with the capture. | `"8e18afdf-db79-449b-b4f5-ee4f14d9f45e"` |
| `filePath` | `string` | The file path of the recording. | `"https://api.wxcc-us1.cisco.com/v1/captures/query"` |
| `createdTime` | `integer` | The time that the capture event occurred in epoch milliseconds. | `160266966391` |

<a id="recording-available"></a>

### Recording Available

`recording:available`

**Resource Version: recording:1.0.0**

An event indicating that the recording for an interaction is available. This event is additive to `capture:available` and uses the same general payload structure with additional `contactType` and `channelType` fields.

When the beta additive events are enabled for your organization, a recording-ready voice interaction emits both `capture:available` and `recording:available`. These two events share the same event `id` because they fan out from the same internal recording-ready signal.

| Field | Type | Description | Example |
| --- | --- | --- | --- |
| `taskId` | `string` | The task ID associated with the recording. | `"e7506dab-4430-4d1b-8834-e994c9862eed"` |
| `filePath` | `string` | The Captures API path that the integration should use to retrieve the available recording details for the task. | `"https://api.wxcc-us1.cisco.com/v1/captures/query"` |
| `contactType` | `string` | The media family for which the recording is available. | `"telephony"` |
| `channelType` | `string` | The channel type for which the recording is available. | `"telephony"` |
| `createdTime` | `integer` | The time that the recording event occurred in epoch milliseconds. | `1781593896741` |

<a id="transcription-available"></a>

### Transcription Available

`transcription:available`

**Resource Version: transcription:1.0.0**

An event indicating that the transcript for an interaction is available. This event is additive and does not change the existing meaning of `capture:available`.

For voice and digital interactions, more than one `transcription:available` event can be delivered if more than one transcript artifact becomes available for the same task.

| Field | Type | Description | Example |
| --- | --- | --- | --- |
| `taskId` | `string` | The task ID associated with the transcript. | `"e7506dab-4430-4d1b-8834-e994c9862eed"` |
| `filePath` | `string` | The Captures API path that the integration should use to retrieve the available transcript details for the task. | `"https://api.wxcc-us1.cisco.com/v1/captures/query"` |
| `contactType` | `string` | The media family for which the transcript is available. This is `telephony` for voice transcripts and can be a digital channel family or admin-configured digital channel value for digital transcripts. | `"telephony"` |
| `channelType` | `string` | Indicates the channel type of a task. | `"telephony", "chat", "email", "social", "customMessaging", "workItem"` |
| `createdTime` | `integer` | The time that the transcript event occurred in epoch milliseconds. | `1781594954447` |

For capture recovery, consult [Search](https://developer.webex.com/docs/api/v1/search/search) and [List Captures](https://developer.webex.com/docs/api/v1/captures/list-captures).

## Tasks

The task resource represents a request or demand for work from agents. Concretely, a telephony task is an incoming call. Tasks are not considered complete until all parties have wrapped up, i.e., the customer has terminated communication and the agent has completed any summary/“wrap-up” work. Tasks are most commonly initiated by the customer (inbound), but can also be initiated by an agent (outbound). Task APIs support telephony. Custom Messaging and Work Item integrations use the Create Task API for inbound task creation and the Task Messages API for subsequent messages or metadata updates. See [Custom Messaging](https://developer.webex.com/docs/bring-your-own-custom-messaging-channel) and [Work Items](https://developer.webex.com/docs/task-routing-work-items) for the request formats and integration steps.

| Resource | Event | Trigger | Resource version |
| --- | --- | --- | --- |
| `task` | [`task:conference-done`](#task-conference-done) | A conference with another Agent and Customer is completed. However, the task is still in progress with the Customer. | `task:1.0.0` |
| `task` | [`task:conferencing`](#task-conferencing) | A task is being conferenced with another Agent as well as the Customer. | `task:1.0.0` |
| `task` | [`task:connect`](#task-connect) | A task is routed to an agent, and the agent has yet to accept the work. | `task:1.0.0` |
| `task` | [`task:connected`](#task-connected) | A task has been successfully accepted by the Agent. | `task:1.0.0` |
| `task` | [`task:consult-done`](#task-consult-done) | A consult with another Agent is completed, while the Customer is currently on hold. | `task:1.0.0` |
| `task` | [`task:consulting`](#task-consulting) | A task is being consulted with another Agent, while the Customer is currently on hold. | `task:1.0.0` |
| `task` | [`task:ended`](#task-ended) | A task has ended either by the Agent or by the Customer. | `task:1.0.0` |
| `task` | [`task:failed`](#task-failed) | A task operation has failed in the contact center. | `task:1.0.0` |
| `task-message` | [`task-message:appended`](#task-message-appended) | An inbound message or Work Item metadata was appended to the task's conversation. | `task-message:1.0.0` |
| `task-message` | [`task-message:append-failed`](#task-message-append-failed) | An inbound message or Work Item metadata failed to be appended to the task's conversation. | `task-message:1.0.0` |
| `task` | [`task:hold-done`](#task-hold-done) | A task is currently resumed by the Agent. | `task:1.0.0` |
| `task` | [`task:new`](#task-new) | A task is formed. | `task:1.0.0` |
| `task` | [`task:on-hold`](#task-on-hold) | A task is currently on hold since the Agent has placed the Customer on hold. | `task:1.0.0` |
| `task` | [`task:paused`](#task-paused) | A task has been paused. | `task:1.0.0` |
| `task` | [`task:resumed`](#task-resumed) | A paused task has been resumed. | `task:1.0.0` |
| `task` | [`task:parked`](#task-parked) | A task is queued because no agents are currently available to handle the task. | `task:1.0.0` |
| `task` | [`task:conference-transferred`](#task-conference-transferred) | A conference is transferred from one Agent to Another Agent. However, the task is still in progress with the Customer. | `task:1.0.0` |
| `task` | [`task:origin-updated`](#task-origin-updated) | A task is updated with a new caller origin | `task:1.0.0` |

<a id="task-conference-done"></a>

### Task Conference Done

`task:conference-done`

**Resource Version: task:1.0.0**

An event indicating that a conference with another Agent and Customer is completed. However, the task is still in progress with the Customer.

| Field | Type | Description | Example |
| --- | --- | --- | --- |
| `taskId` | `string` | The ID associated with a specific interaction. | `"888b688e-b74e-4fa6-8260-1e8d0a3523a"` |
| `origin` | `string` | Customer’s channel-specific identifier.<br />For telephony, this is the phone number.<br />For email and chat, this is the email address. | `"1+9****8095"` |
| `destination` | `string` | Destination the customer contacted.<br />For telephony, this is the number the customer called.<br />For chat, this is the chat template name where the chat takes place.<br />For email, it is the email address contacted. | `"1+5****2001"` |

<a id="task-conferencing"></a>

### Task Conferencing

`task:conferencing`

**Resource Version: task:1.0.0**

An event indicating that a task is being conferenced with another Agent as well as the Customer.

| Field | Type | Description | Example |
| --- | --- | --- | --- |
| `taskId` | `string` | The ID associated with a specific interaction. | `"888b688e-b74e-4fa6-8260-1e8d0a3523a"` |
| `origin` | `string` | Customer’s channel-specific identifier.<br />For telephony, this is the phone number.<br />For email and chat, this is the email address. | `"1+9****8095"` |
| `destination` | `string` | Destination the customer contacted.<br />For telephony, this is the number the customer called.<br />For chat, this is the chat template name where the chat takes place.<br />For email, it is the email address contacted. | `"1+5****2001"` |
| `direction` | `string` | Indicates which party initiated the Task.<br />If **"INBOUND"**, it was initiated by the customer.<br />If **"OUTBOUND"**, it was initiated by the system or an agent. | `"INBOUND"` |
| `channelType` | `string` | Indicates the channel type of a task. | `"telephony\|chat\|email\|social"` |
| `outboundType` | `string` | Indicates if the outbound task was an autodial, campaign, or callback. | `null` |
| `queueId` | `string` | The ID associated with an agent queue. | `"AXbm0MeV1O4n5kITbT6"` |
| `createdTime` | `integer` | The time at which the event occurred in epoch milliseconds. | `160269663691` |

<a id="task-connect"></a>

### Task Connect

`task:connect`

**Resource Version: task:1.0.0**

An event indicating that a task is routed to an agent, and the agent has yet to accept the work.

| Field | Type | Description | Example |
| --- | --- | --- | --- |
| `taskId` | `string` | The ID associated with a specific interaction. | `"888b688e-b74e-4fa6-8260-1e8d0a3523a"` |
| `origin` | `string` | Customer’s channel-specific identifier.<br />For telephony, this is the phone number.<br />For email and chat, this is the email address. | `"1+9****8095"` |
| `destination` | `string` | Destination the customer contacted.<br />For telephony, this is the number the customer called.<br />For chat, this is the chat template name where the chat takes place.<br />For email, it is the email address contacted. | `"1+5****2001"` |
| `direction` | `string` | Indicates which party initiated the Task.<br />If **"INBOUND"**, it was initiated by the customer.<br />If **"OUTBOUND"**, it was initiated by the system or an agent. | `"INBOUND"` |
| `channelType` | `string` | Indicates the channel type of a task. | `"telephony\|chat\|email\|social"` |
| `outboundType` | `string` | Indicates if the outbound task was an autodial, campaign, or callback. | `null` |
| `queueId` | `string` | The ID associated with an agent queue. | `"AXbm0MeV1O4n5kITbT6"` |
| `createdTime` | `integer` | The time at which the event occurred in epoch milliseconds. | `160269663691` |

<a id="task-connected"></a>

### Task Connected

`task:connected`

**Resource Version: task:1.0.0**

An event indicating that a task has been successfully accepted by the Agent.

| Field | Type | Description | Example |
| --- | --- | --- | --- |
| `taskId` | `string` | The ID associated with a specific interaction. | `"888b688e-b74e-4fa6-8260-1e8d0a3523a"` |
| `origin` | `string` | Customer’s channel-specific identifier.<br />For telephony, this is the phone number.<br />For email and chat, this is the email address. | `"1+9****8095"` |
| `destination` | `string` | Destination the customer contacted.<br />For telephony, this is the number the customer called.<br />For chat, this is the chat template name where the chat takes place.<br />For email, it is the email address contacted. | `"1+5****2001"` |
| `direction` | `string` | Indicates which party initiated the Task.<br />If **"INBOUND"**, it was initiated by the customer.<br />If **"OUTBOUND"**, it was initiated by the system or an agent. | `"INBOUND"` |
| `channelType` | `string` | Indicates the channel type of a task. | `"telephony\|chat\|email\|social"` |
| `outboundType` | `string` | Indicates if the outbound task was an autodial, campaign, or callback. | `null` |
| `queueId` | `string` | The ID associated with an agent queue. | `"AXbm0MeV1O4n5kITbT6"` |
| `createdTime` | `integer` | The time at which the event occurred in epoch milliseconds. | `160269663691` |

<a id="task-consult-done"></a>

### Task Consult Done

`task:consult-done`

**Resource Version: task:1.0.0**

An event indicating that a consult with another Agent is completed, while the Customer is currently on hold.

| Field | Type | Description | Example |
| --- | --- | --- | --- |
| `taskId` | `string` | The ID associated with a specific interaction. | `"888b688e-b74e-4fa6-8260-1e8d0a3523a"` |
| `origin` | `string` | Customer’s channel-specific identifier.<br />For telephony, this is the phone number.<br />For email and chat, this is the email address. | `"1+9****8095"` |
| `destination` | `string` | Destination the customer contacted.<br />For telephony, this is the number the customer called.<br />For chat, this is the chat template name where the chat takes place.<br />For email, it is the email address contacted. | `"1+5****2001"` |
| `direction` | `string` | Indicates which party initiated the Task.<br />If **"INBOUND"**, it was initiated by the customer.<br />If **"OUTBOUND"**, it was initiated by the system or an agent. | `"INBOUND"` |
| `channelType` | `string` | Indicates the channel type of a task. | `"telephony\|chat\|email\|social"` |
| `outboundType` | `string` | Indicates if the outbound task was an autodial, campaign, or callback. | `null` |
| `queueId` | `string` | The ID associated with an agent queue. | `"AXbm0MeV1O4n5kITbT6"` |
| `createdTime` | `integer` | The time at which the event occurred in epoch milliseconds. | `160269663691` |

<a id="task-consulting"></a>

### Task Consulting

`task:consulting`

**Resource Version: task:1.0.0**

An event indicating that a task is being consulted with another Agent, while the Customer is currently on hold.

| Field | Type | Description | Example |
| --- | --- | --- | --- |
| `taskId` | `string` | The ID associated with a specific interaction. | `"888b688e-b74e-4fa6-8260-1e8d0a3523a"` |
| `origin` | `string` | Customer’s channel-specific identifier.<br />For telephony, this is the phone number.<br />For email and chat, this is the email address. | `"1+9****8095"` |
| `destination` | `string` | Destination the customer contacted.<br />For telephony, this is the number the customer called.<br />For chat, this is the chat template name where the chat takes place.<br />For email, it is the email address contacted. | `"1+5****2001"` |
| `direction` | `string` | Indicates which party initiated the Task.<br />If **"INBOUND"**, it was initiated by the customer.<br />If **"OUTBOUND"**, it was initiated by the system or an agent. | `"INBOUND"` |
| `channelType` | `string` | Indicates the channel type of a task. | `"telephony\|chat\|email\|social"` |
| `outboundType` | `string` | Indicates if the outbound task was an autodial, campaign, or callback. | `null` |
| `queueId` | `string` | The ID associated with an agent queue. | `"AXbm0MeV1O4n5kITbT6"` |
| `createdTime` | `integer` | The time at which the event occurred in epoch milliseconds. | `160269663691` |

<a id="task-ended"></a>

### Task Ended

`task:ended`

**Resource Version: task:1.0.0**

An event indicating that a task has ended either by the Agent or by the Customer.

| Field | Type | Description | Example |
| --- | --- | --- | --- |
| `taskId` | `string` | The ID associated with a specific interaction. | `"888b688e-b74e-4fa6-8260-1e8d0a3523a"` |
| `origin` | `string` | Customer’s channel-specific identifier.<br />For telephony, this is the phone number.<br />For email and chat, this is the email address.<br />For Custom Messaging and Work Items, this is the customer or source-system identifier supplied in `origin.address`. | `"1+9****8095"` |
| `destination` | `string` | Destination the customer contacted.<br />For telephony, this is the number the customer called.<br />For chat, this is the chat template name where the chat takes place.<br />For email, it is the email address contacted.<br />For Custom Messaging and Work Items, this is the business address configured on the asset. | `"1+5****2001"` |
| `direction` | `string` | Indicates which party initiated the Task.<br />If **"INBOUND"**, it was initiated by the customer.<br />If **"OUTBOUND"**, it was initiated by the system or an agent. | `"INBOUND"` |
| `channelType` | `string` | Indicates the channel type of a task. | `"telephony\|chat\|email\|social\|customMessaging\|workItem"` |
| `outboundType` | `string` | Indicates if the outbound task was an autodial, campaign, or callback. | `null` |
| `terminatingParty` | `string` | Indicates which party ended the task. Can be an Agent or a Customer. | `"Customer\|Agent"` |
| `reason` | `string` | Indicates the cause for a task to end. | `"Agent left\|Customer left"` |
| `queueId` | `string` | The ID associated with an agent queue. | `"AXbm0MeV1O4n5kITbT6"` |
| `createdTime` | `integer` | The time at which the event occurred in epoch milliseconds. | `160269663691` |

<a id="task-failed"></a>

### Task Failed

`task:failed`

**Resource Version: task:1.0.0**

An event indicating that a task operation has failed in the contact center. For Custom Messaging and Work Items, it reports a task-creation failure after the Create Task request was accepted. Some validation or access failures are returned directly in the HTTP response before acceptance and do not produce this notification.

For complete notification examples, see the [Custom Messaging guide](https://developer.webex.com/docs/bring-your-own-custom-messaging-channel#subscribe-to-task-lifecycle-events) and [Work Item guide](https://developer.webex.com/docs/task-routing-work-items#webhook-events).

The field table includes fields used by different task failure paths. Fields such as `mediaMgr`, `mediaChannel`, `mediaResourceId` and `fcScriptId` are not present in every payload.

| Field | Type | Description | Example |
| --- | --- | --- | --- |
| `taskId` | `string` | The ID associated with the task operation. Use this value for correlation with related task operations and events. | `"888b688e-b74e-4fa6-8260-1e8d0a3523a"` |
| `origin` | `string, optional` | Customer endpoint address.<br />For telephony, this is the phone number.<br />For email, this is the email address.<br />For social, this is the customer's social identifier.<br />For customMessaging, this is the customer identifier from the external messaging channel.<br />For workItem, this is the source-system identifier supplied in `origin.address`. | `"customer@example.com"` |
| `destination` | `string, optional` | Customer care endpoint address.<br />For telephony, this is the number the customer called.<br />For chat, this is the chat template name where the chat takes place.<br />For email, it is the email address contacted.<br />For customMessaging, this is the business address configured on the Custom Messaging asset.<br />For workItem, this is the business address configured on the Work Item asset. | `"support@channel.biz"` |
| `direction` | `string, optional` | Indicates which party initiated the Task.<br />If **"INBOUND"**, it was initiated by the customer.<br />If **"OUTBOUND"**, it was initiated by the system or an agent.<br />Custom Messaging and Work Item creation failures use lowercase `inbound`. | `"INBOUND"`, `"inbound"` |
| `channelType` | `string, optional` | The media type of the task. | `"chat\|email\|social\|workItem\|customMessaging"` |
| `channel` | `string, optional` | Configured Custom Messaging or Work Item channel name, when available. | `"my-custom-channel"` |
| `mediaMgr` | `string, optional` | The name of the media manager responsible for handling the task. Omitted from Custom Messaging and Work Item creation-failure notifications. | `"digitalmm"` |
| `mediaChannel` | `string, optional` | The specific media channel within the media type. | `"facebook"` |
| `mediaResourceId` | `string, optional` | The media resource identifier associated with the task, if applicable. | `"e2f3a4b5-c6d7-8e9f-0a1b-2c3d4e5f6789"` |
| `fcScriptId` | `string, optional` | The entry point ID associated with the task's flow control script. | `"AXCLfX19Id7K1N9hMlfR"` |
| `reason` | `string, optional` | Partner-visible failure reason. Treat this as a representative runtime value, not as an exhaustive list. | `"CONVERSATION_ALREADY_OPEN"` |
| `errorMessage` | `string, optional` | Human-readable error message returned for the failure. This should be treated as representative and may vary by failure path. | `"Conversation is already open with task id ab4ea619-a1ad-33a3-aed9-c2563a9bd6cc"` |
| `failureType` | `string, optional` | Failure state published for the task. For Custom Messaging and Work Items, `failed` indicates a processing failure; `rejected` indicates that task creation was refused, for example because the organization’s active digital contact limit was reached. | `"failed"`, `"rejected"` |
| `createdTime` | `integer` | The time at which the event occurred in epoch milliseconds. | `160269663691` |

<a id="task-message-appended"></a>

### Task Message Appended

`task-message:appended`

**Resource Version: task-message:1.0.0**

An event indicating that an inbound message has been successfully appended to a task's conversation. For Custom Messaging, this acknowledges the initial inbound message or a subsequent customer message. For Work Items, it acknowledges the initial Work Item data or a subsequent metadata update.

This section covers subscription notifications. Webhooks for outbound messages sent by a flow or an agent are delivered to the webhook URL configured on the Custom Messaging asset. See the [Custom Messaging guide](https://developer.webex.com/docs/bring-your-own-custom-messaging-channel#receive-outbound-partner-webhooks).

For a Task Messages API request, correlate the notification's envelope `id` with the API response `data.id`. Use `data.taskId` to identify the task. For the initial message, correlate `data.taskId` with the Create Task response `data.id`. A message's `messageId`, its `aliasId` and the notification's `id` are separate identifiers and must not be assumed to match.

For complete notification examples, see the [Custom Messaging guide](https://developer.webex.com/docs/bring-your-own-custom-messaging-channel#subscribe-to-task-lifecycle-events) and [Work Item guide](https://developer.webex.com/docs/task-routing-work-items#webhook-events).

The following fields describe the notification's `data` object. Nested paths such as `channelProperties.message.aliasId` are relative to `data`.

| Field | Type | Description | Example |
| --- | --- | --- | --- |
| `taskId` | `string` | Task identifier returned by Create Task. | `"141897a0-6212-49be-be9d-4823ab1e4dc7"` |
| `direction` | `string, optional` | Direction of the task; `INBOUND` for the Custom Messaging and Work Item tasks described here. | `"INBOUND"` |
| `channelType` | `string, optional` | Type of the task's channel. | `"customMessaging"`, `"workItem"` |
| `channel` | `string, optional` | Configured channel name. | `"my-custom-channel"`, `"ClaimsReview"` |
| `origin` | `string, optional` | Customer or source-system identifier supplied in Create Task. | `"customer@example.com"`, `"crm-lead-10040"` |
| `destination` | `string, optional` | Business address configured on the Custom Messaging or Work Item asset. | `"support@channel.biz"`, `"claims-work-items@example.biz"` |
| `createdTime` | `integer, optional` | Notification creation time in epoch milliseconds. Use the nested message timestamp for the original message time. | `1779789108999` |
| `eventDetails` | `string, optional` | Status summary when available. | `"Appended Work Item data successfully."` |
| `channelProperties` | `object, optional` | Channel and message metadata, with security results when applicable. Custom Messaging notifications omit `message.text` and `message.attachments`; Work Item notifications omit `message.workItemData`. | See channel and message fields below. |
| `channelProperties.channelType` | `string, optional` | Channel type inside the message envelope. | `"customMessaging"`, `"workItem"` |
| `channelProperties.channel` | `string, optional` | Configured channel name inside the message envelope. | `"my-custom-channel"`, `"ClaimsReview"` |
| `channelProperties.message.messageId` | `string, optional` | Webex message identifier. | `"44444444-4444-4444-8444-444444444444"` |
| `channelProperties.message.aliasId` | `string, optional` | Supplied or generated message alias. A supplied alias need not be a UUID. | `"partner-update-002"` |
| `channelProperties.message.direction` | `string, optional` | Message direction, using lowercase `inbound` for these notifications. | `"inbound"` |
| `channelProperties.message.type` | `string, optional` | For Custom Messaging: `text` or `text-with-attachments`.<br />For Work Items: `work-item`. | `"text"`, `"text-with-attachments"`, `"work-item"` |
| `channelProperties.message.timestamp` | `string, optional` | Original message time in ISO format. | `"2026-05-26T09:51:48.649Z"` |
| `channelProperties.message.timestampEpoch` | `integer, optional` | Original message time in epoch milliseconds. | `1779789108649` |
| `channelProperties.securityComplianceInfo` | `object or null, optional` | Custom Messaging security results when available. Always `null` for Work Item messages because Work Item data is not scanned for PCI or malware. | See security fields below; `null` for Work Items. |

The notification acknowledges processing without returning the submitted message content. Validated Custom Messaging content is available to the flow through Start and Receive nodes. The initial Work Item data is available through the Start node. Keep the submitted content in your integration if it is needed when processing the notification.

For Custom Messaging, a successful append can include masked text or dropped attachments. Inspect the security results to understand which checks ran and their outcomes. The following fields can appear inside `data.channelProperties.securityComplianceInfo`:

| Field | Type | Description | Example |
| --- | --- | --- | --- |
| `droppedAttachmentCount` | `integer` | Total number of dropped attachments. | `0` |
| `malwareScan.isCompliant` | `boolean` | Malware compliance result; interpret together with `validationDone`. | `true` |
| `malwareScan.validationDone` | `boolean` | Whether malware validation completed. | `true` |
| `malwareScan.droppedAttachmentCount` | `integer` | Number of attachments dropped by malware validation. | `0` |
| `malwareScan.files` | `object[], optional` | Details of files affected by malware validation. | See file result fields below. |
| `malwareScan.files[].name` | `string` | Name of the file affected by malware validation. | `"blocked-file.pdf"` |
| `malwareScan.files[].errorCode` | `string` | Malware validation failure code. | `"MALWARE_DETECTED"` |
| `malwareScan.files[].errorMsg` | `string` | Explanation of the malware validation failure. | `"Malware was detected"` |
| `pciScan.isCompliant` | `boolean` | PCI compliance result; interpret together with `validationDone` and `textRedacted`. | `true` |
| `pciScan.validationDone` | `boolean` | Whether PCI validation completed. | `true` |
| `pciScan.textRedacted` | `boolean` | Whether PCI-sensitive message text was masked. The notification does not contain the text. | `false` |
| `pciScan.droppedAttachmentCount` | `integer` | Number of attachments dropped by PCI validation. | `0` |
| `pciScan.files` | `object[], optional` | Details of files affected by PCI validation. | See file result fields below. |
| `pciScan.files[].name` | `string` | Name of the file affected by PCI validation. | `"customer-document.pdf"` |
| `pciScan.files[].errorCode` | `string` | PCI validation failure code. | `"PCI_CONTENT_DETECTED"` |
| `pciScan.files[].errorMsg` | `string` | Explanation returned by PCI validation. | `"Attachment violates data security policy"` |

Work Item notifications do not contain scan results: their `securityComplianceInfo` value is always `null`.

<a id="task-message-append-failed"></a>

### Task Message Append Failed

`task-message:append-failed`

**Resource Version: task-message:1.0.0**

An event indicating that an inbound message failed to be appended to a task's conversation. For Work Items, this refers to a metadata update. The notification reports processing failures after the Task Messages API request was accepted. Requests rejected directly in the HTTP response do not necessarily produce this notification.

For complete notification examples, see the [Custom Messaging guide](https://developer.webex.com/docs/bring-your-own-custom-messaging-channel#subscribe-to-task-lifecycle-events) and [Work Item guide](https://developer.webex.com/docs/task-routing-work-items#webhook-events).

Correlate the notification's envelope `id` with the Task Messages API response `data.id`, and use `data.taskId` to identify the task. The field table below describes `data`.

| Field | Type | Description | Example |
| --- | --- | --- | --- |
| `taskId` | `string` | The ID associated with the task for which the append operation failed. | `"141897a0-6212-49be-be9d-4823ab1e4dc7"` |
| `direction` | `string, optional` | Direction of the task when available. | `"INBOUND"` |
| `channelType` | `string, optional` | Task channel type when available. | `"customMessaging"`, `"workItem"` |
| `channel` | `string, optional` | Configured channel name associated with the task when available. | `"my-custom-channel"`, `"ClaimsReview"` |
| `origin` | `string, optional` | Customer or source-system identifier when available. | `"customer@example.com"`, `"crm-lead-10040"` |
| `destination` | `string, optional` | Business address associated with the task when available. | `"support@channel.biz"`, `"claims-work-items@example.biz"` |
| `createdTime` | `integer, optional` | Notification creation time in epoch milliseconds. | `1779789108999` |
| `reason` | `string, optional` | Partner-visible failure reason. Treat documented values as representative, not exhaustive. | `"INVALID_CONTENT"` |
| `errorMessage` | `string, optional` | Human-readable failure detail. | `"channelProperties.channel must match the channel specified in the Create Task request."` |

Common inbound append-failure categories include `NOT_FOUND`, `INVALID_CONTENT` and `INTERNAL_ERROR`.

Append-failure notifications contain error metadata without `channelProperties`. Inspect `reason` and `errorMessage`, correct validation failures before retrying, and verify the task ID when `NOT_FOUND` is reported. A channel or channel-type mismatch can be reported as `INVALID_CONTENT` after HTTP acceptance.

For request formats and message-identifier behavior, see the [Custom Messaging guide](https://developer.webex.com/docs/bring-your-own-custom-messaging-channel#append-subsequent-inbound-messages) and [Work Item guide](https://developer.webex.com/docs/task-routing-work-items#update-work-item-data).

<a id="task-hold-done"></a>

### Task Hold Done

`task:hold-done`

**Resource Version: task:1.0.0**

An event indicating that a task is currently resumed by the Agent.

| Field | Type | Description | Example |
| --- | --- | --- | --- |
| `taskId` | `string` | The ID associated with a specific interaction. | `"888b688e-b74e-4fa6-8260-1e8d0a3523a"` |
| `origin` | `string` | Customer’s channel-specific identifier.<br />For telephony, this is the phone number.<br />For email and chat, this is the email address. | `"1+9****8095"` |
| `destination` | `string` | Destination the customer contacted.<br />For telephony, this is the number the customer called.<br />For chat, this is the chat template name where the chat takes place.<br />For email, it is the email address contacted. | `"1+5****2001"` |
| `direction` | `string` | Indicates which party initiated the Task.<br />If **"INBOUND"**, it was initiated by the customer.<br />If **"OUTBOUND"**, it was initiated by the system or an agent. | `"INBOUND"` |
| `channelType` | `string` | Indicates the channel type of a task. | `"telephony\|chat\|email\|social"` |
| `outboundType` | `string` | Indicates if the outbound task was an autodial, campaign, or callback. | `null` |
| `queueId` | `string` | The ID associated with an agent queue. | `"AXbm0MeV1O4n5kITbT6"` |
| `createdTime` | `integer` | The time at which the event occurred in epoch milliseconds. | `160269663691` |

<a id="task-new"></a>

### Task New

`task:new`

**Resource Version: task:1.0.0**

An event indicating that a task is formed.

| Field | Type | Description | Example |
| --- | --- | --- | --- |
| `taskId` | `string` | The ID associated with a specific interaction. | `"888b688e-b74e-4fa6-8260-1e8d0a3523a"` |
| `origin` | `string` | Customer’s channel-specific identifier.<br />For telephony, this is the phone number.<br />For email and chat, this is the email address.<br />For Custom Messaging and Work Items, this is the customer or source-system identifier supplied in `origin.address`. | `"1+9****8095"` |
| `destination` | `string` | Destination the customer contacted.<br />For telephony, this is the number the customer called.<br />For chat, this is the chat template name where the chat takes place.<br />For email, it is the email address contacted.<br />For Custom Messaging and Work Items, this is the business address configured on the asset. | `"1+5****2001"` |
| `direction` | `string` | Indicates which party initiated the Task.<br />If **"INBOUND"**, it was initiated by the customer.<br />If **"OUTBOUND"**, it was initiated by the system or an agent. | `"INBOUND"` |
| `channelType` | `string` | Indicates the channel type of a task. | `"telephony\|chat\|email\|social\|customMessaging\|workItem"` |
| `outboundType` | `string` | Indicates if the outbound task was an autodial, campaign, or callback. | `null` |
| `createdTime` | `integer` | The time at which the event occurred in epoch milliseconds. | `160269663691` |

For Custom Messaging and Work Items, correlate `taskId` with the Create Task response `data.id`. This event confirms that the task was formed. A separate `task-message:appended` notification acknowledges the initial inbound message or Work Item data. The `task:new` payload does not contain the message content or Work Item form.

<a id="task-on-hold"></a>

### Task On Hold

`task:on-hold`

**Resource Version: task:1.0.0**

An event indicating that a task is currently on hold since the Agent has placed the Customer on hold.

| Field | Type | Description | Example |
| --- | --- | --- | --- |
| `taskId` | `string` | The ID associated with a specific interaction. | `"888b688e-b74e-4fa6-8260-1e8d0a3523a"` |
| `origin` | `string` | Customer’s channel-specific identifier.<br />For telephony, this is the phone number.<br />For email and chat, this is the email address. | `"1+9****8095"` |
| `destination` | `string` | Destination the customer contacted.<br />For telephony, this is the number the customer called.<br />For chat, this is the chat template name where the chat takes place.<br />For email, it is the email address contacted. | `"1+5****2001"` |
| `direction` | `string` | Indicates which party initiated the Task.<br />If **"INBOUND"**, it was initiated by the customer.<br />If **"OUTBOUND"**, it was initiated by the system or an agent. | `"INBOUND"` |
| `channelType` | `string` | Indicates the channel type of a task. | `"telephony\|chat\|email\|social"` |
| `outboundType` | `string` | Indicates if the outbound task was an autodial, campaign, or callback. | `null` |
| `queueId` | `string` | The ID associated with an agent queue. | `"AXbm0MeV1O14n5KIbT6"` |
| `createdTime` | `integer` | The time at which the event occurred in epoch milliseconds. | `160269663691` |

<a id="task-paused"></a>

### Task Paused

`task:paused`

**Resource Version: task:1.0.0**

An event indicating that a task has been paused.

| Field | Type | Description | Example |
| --- | --- | --- | --- |
| `createdTime` | `integer` | The time at which the event occurred in epoch milliseconds. | `1782143191122` |
| `taskId` | `string` | The ID associated with the task. | `"c6563fda-38a7-48f8-b4d7-dffc30f0623b"` |
| `channelType` | `string` | The channel type of the task. | `"email"` |
| `direction` | `string` | Indicates which party initiated the task. | `"INBOUND"` |
| `origin` | `string` | Customer endpoint address. | `"customer@example.com"` |
| `destination` | `string` | Customer care endpoint address. | `"support@channel.biz"` |
| `queueId` | `string` | The ID associated with the agent queue. | `"AXlp8E3f-KJXJ6KOPIK"` |
| `agentId` | `string` | The ID associated with the Agent handling the task. | `"153794be-5d22-406d-8b01-fc2753ed5e8a"` |

<a id="task-resumed"></a>

### Task Resumed

`task:resumed`

**Resource Version: task:1.0.0**

An event indicating that a paused task has been resumed.

| Field | Type | Description | Example |
| --- | --- | --- | --- |
| `createdTime` | `integer` | The time at which the event occurred in epoch milliseconds. | `1782143191144` |
| `taskId` | `string` | The ID associated with the task. | `"c6563fda-38a7-48f8-b4d7-dffc30f0623c"` |
| `channelType` | `string` | The channel type of the task. | `"email"` |
| `direction` | `string` | Indicates which party initiated the task. | `"INBOUND"` |
| `origin` | `string` | Customer endpoint address. | `"customer@example.com"` |
| `destination` | `string` | Customer care endpoint address. | `"support@channel.biz"` |
| `queueId` | `string` | The ID associated with the agent queue. | `"AXlp8E3f-KJXJ6KOPIK"` |
| `agentId` | `string` | The ID associated with the Agent handling the task. | `"153794be-5d22-406d-8b01-fc2753ed5e8a"` |

<a id="task-parked"></a>

### Task Parked

`task:parked`

**Resource Version: task:1.0.0**

An event indicating that a task is queued because no agents are currently available to handle the task.

| Field | Type | Description | Example |
| --- | --- | --- | --- |
| `taskId` | `string` | The ID associated with a specific interaction. | `"888b688e-b74e-4fa6-8260-1e8d0a3523a"` |
| `origin` | `string` | Customer’s channel-specific identifier.<br />For telephony, this is the phone number.<br />For email and chat, this is the email address. | `"1+9****8095"` |
| `destination` | `string` | Destination the customer contacted.<br />For telephony, this is the number the customer called.<br />For chat, this is the chat template name where the chat takes place.<br />For email, it is the email address contacted. | `"1+5****2001"` |
| `direction` | `string` | Indicates which party initiated the Task.<br />If **"INBOUND"**, it was initiated by the customer.<br />If **"OUTBOUND"**, it was initiated by the system or an agent. | `"INBOUND"` |
| `channelType` | `string` | Indicates the channel type of a task. | `"telephony\|chat\|email\|social"` |
| `outboundType` | `string` | Indicates if the outbound task was an autodial, campaign, or callback. | `null` |
| `queueId` | `string` | The ID associated with an agent queue. | `"AXbm0MeV1OI4n5kITbT6"` |
| `createdTime` | `integer` | The time at which the event occurred in epoch milliseconds. | `1602696696391` |

<a id="task-conference-transferred"></a>

### Task Conference Transferred

`task:conference-transferred`

**Resource Version: task:1.0.0**

An event indicating that a conference is transferred from one Agent to Another Agent. However, the task is still in progress with the Customer.

| Field | Type | Description | Example |
| --- | --- | --- | --- |
| `taskId` | `string` | The ID associated with a specific interaction. | `"888b688e-b74e-4fa6-8260-1e8d0a3523a"` |
| `origin` | `string` | Customer’s channel-specific identifier.<br />For telephony, this is the phone number.<br />For email and chat, this is the email address. | `"1+9****8095"` |
| `destination` | `string` | Destination the customer contacted.<br />For telephony, this is the number the customer called.<br />For chat, this is the chat template name where the chat takes place.<br />For email, it is the email address contacted. | `"1+5****2001"` |
| `direction` | `string` | Indicates which party initiated the Task.<br />If **"INBOUND"**, it was initiated by the customer.<br />If **"OUTBOUND"**, it was initiated by the system or an agent. | `"INBOUND"` |
| `channelType` | `string` | Indicates the channel type of a task. | `"telephony\|chat\|email\|social"` |
| `outboundType` | `string` | Indicates if the outbound task was an autodial, campaign, or callback. | `null` |
| `queueId` | `string` | The ID associated with an agent queue. | `"AXbm0MeV1OI4n5kITbT6"` |
| `createdTime` | `integer` | The time at which the event occurred in epoch milliseconds. | `1602696696391` |

<a id="task-origin-updated"></a>

### Task Origin Updated

`task:origin-updated`

**Resource Version: task:1.0.0**

An event indicating that a task is updated with a new caller origin

| Field | Type | Description | Example |
| --- | --- | --- | --- |
| `taskId` | `string` | The ID associated with a specific interaction. | `"888b688e-b74e-4fa6-8260-1e8d0a3523a"` |
| `origin` | `string` | Customer’s channel-specific identifier.<br />For telephony, this is the phone number.<br />For email and chat, this is the email address. | `"1+9****8095"` |
| `destination` | `string` | Destination the customer contacted.<br />For telephony, this is the number the customer called.<br />For chat, this is the chat template name where the chat takes place.<br />For email, it is the email address contacted. | `"1+5****2001"` |
| `direction` | `string` | Indicates which party initiated the Task.<br />If **"INBOUND"**, it was initiated by the customer.<br />If **"OUTBOUND"**, it was initiated by the system or an agent. | `"INBOUND"` |
| `channelType` | `string` | Indicates the channel type of a task. | `"telephony\|chat\|email\|social"` |
| `queueId` | `string` | The ID associated with an agent queue. | `"AXbm0MeV1O14n5KIbT6"` |
| `createdTime` | `integer` | The time at which the event occurred in epoch milliseconds. | `160269663691` |

## Flows

The flow resource represents a published Webex Contact Center Flow Designer execution. A flow defines the routing and orchestration logic that runs for a customer interaction, including IVR prompts, queueing decisions, data dips, virtual agent steps, event handling, and downstream routing actions.

| Resource | Event | Trigger | Resource version |
| --- | --- | --- | --- |
| `flow` | [`flow:error`](#flow-error) | A Flow Designer flow encountered an error during execution. | `flow:1.0.0` |

Flow webhooks provide observability events for flow execution outcomes. The `flow:error` webhook is sent when a flow encounters an error during execution. This event is designed for failure scenarios and helps administrators and developers monitor failed flow executions, investigate issues faster, and take action when a flow fails.

The `flow:error` webhook delivers targeted error observability data that can be sent to platforms such as Splunk or other third-party analytics and observability solutions. It is not intended to stream all flow debug or execution data. Use this webhook to monitor actionable flow failures in near real time and to trigger downstream alerting, investigation, or automation workflows.

Customers can manage HTTPS webhook collector URLs in **Developer Portal > Webhooks** to support secure delivery of flow error events to external observability platforms.

<a id="flow-error"></a>

### Flow Error

`flow:error`

**Resource Version: flow:1.0.0**

An event indicating that a Flow Designer flow encountered an error during execution.

Use this event to observe failed flow executions, correlate failures to affected interactions, and route failure details into external observability tools. This event is emitted only for flow failure scenarios and does not include complete flow debug traces or all activity-level execution data.

| Field | Type | Description | Example |
| --- | --- | --- | --- |
| `interactionId` | `string` | The ID associated with the interaction in which the flow error occurred. | `"44af0d2a-2ef4-4049-a402-e41939d72f4d"` |
| `flowId` | `string` | The ID associated with the flow that encountered the error. | `"684a72233daf36734cb5c499"` |
| `flowVersionId` | `string` | The ID associated with the published flow version that was executing when the error occurred. | `"68510a9f3daf36734cb5c72b"` |
| `tagName` | `string` | The flow tag associated with the executing flow version. | `"Latest"` |
| `activityName` | `string` | The name of the Flow Designer activity where the error occurred. | `"GetQueueInfo_hdt"` |
| `startTime` | `integer` | The time at which the failed activity started, in epoch milliseconds. | `1750855852249` |
| `endTime` | `integer` | The time at which the failed activity ended, in epoch milliseconds. | `1750855852376` |
| `status` | `string` | The flow execution status for this event. | `"error"` |
| `statusDescription` | `string` | The description or reason associated with the error status. | `"INSUFFICIENT_DATA"` |
| `debugUrl` | `string` | The URL that can be used to open the failed interaction in Flow Designer debug mode. | `"https://flow-control.prodjp1.ciscoccservice.com/flow/{flowId}/debug/{interactionId}?orgId={orgId}&version={flowVersionId}"` |
| `createdTime` | `integer` | The time at which the flow error event was created, in epoch milliseconds. | `1750855852391` |

## Interpret payloads

Every event uses the [common Contact Center webhook envelope](https://developer.webex.com/docs/receive-and-verify-contact-center-webhooks#anatomy-of-a-webhook). Its `type` is the event identifier shown above, such as `agent:login` or `task:connected`. The field tables describe the contents of `data`.

Field types, optional markers, and examples are event-specific. Preserve field names, casing, and timestamp units. Do not infer a shared payload schema or required fields from another event's example.

See the receiver guide for [signature verification](https://developer.webex.com/docs/receive-and-verify-contact-center-webhooks#request-verification) and [delivery acknowledgements](https://developer.webex.com/docs/receive-and-verify-contact-center-webhooks#response).
