---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webhooks-cc
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Tasks
- Task Consulting
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webhooks-cc). [Full Markdown](../../../../docs/webhooks-cc.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Find Webex Contact Center webhook event types, resource versions, and event-specific payload fields.

---

<a id="using-webhooks"></a>

<a id="overview"></a>

## Parent context

## Tasks

The task resource represents a request or demand for work from agents. Concretely, a telephony task is an incoming call. Tasks are not considered complete until all parties have wrapped up, i.e., the customer has terminated communication and the agent has completed any summary/“wrap-up” work. Tasks are most commonly initiated by the customer (inbound), but can also be initiated by an agent (outbound). Presently, Task APIs are supported for telephony media only.

| Resource | Event | Trigger | Resource version |
| --- | --- | --- | --- |
| `task` | [`task:conference-done`](https://developer.webex.com/docs/webhooks-cc#task-conference-done) | A conference with another Agent and Customer is completed. However, the task is still in progress with the Customer. | `task:1.0.0` |
| `task` | [`task:conferencing`](https://developer.webex.com/docs/webhooks-cc#task-conferencing) | A task is being conferenced with another Agent as well as the Customer. | `task:1.0.0` |
| `task` | [`task:connect`](https://developer.webex.com/docs/webhooks-cc#task-connect) | A task is routed to an agent, and the agent has yet to accept the work. | `task:1.0.0` |
| `task` | [`task:connected`](https://developer.webex.com/docs/webhooks-cc#task-connected) | A task has been successfully accepted by the Agent. | `task:1.0.0` |
| `task` | [`task:consult-done`](https://developer.webex.com/docs/webhooks-cc#task-consult-done) | A consult with another Agent is completed, while the Customer is currently on hold. | `task:1.0.0` |
| `task` | [`task:consulting`](https://developer.webex.com/docs/webhooks-cc#task-consulting) | A task is being consulted with another Agent, while the Customer is currently on hold. | `task:1.0.0` |
| `task` | [`task:ended`](https://developer.webex.com/docs/webhooks-cc#task-ended) | A task has ended either by the Agent or by the Customer. | `task:1.0.0` |
| `task` | [`task:failed`](https://developer.webex.com/docs/webhooks-cc#task-failed) | A task operation has failed in the contact center. | `task:1.0.0` |
| `task-message` | [`task-message:appended`](https://developer.webex.com/docs/webhooks-cc#task-message-appended) | An inbound message was appended to the task's conversation. | `task-message:1.0.0` |
| `task-message` | [`task-message:append-failed`](https://developer.webex.com/docs/webhooks-cc#task-message-append-failed) | An inbound message could not be appended to the task's conversation. | `task-message:1.0.0` |
| `task` | [`task:hold-done`](https://developer.webex.com/docs/webhooks-cc#task-hold-done) | A task is currently resumed by the Agent. | `task:1.0.0` |
| `task` | [`task:new`](https://developer.webex.com/docs/webhooks-cc#task-new) | A task is formed. | `task:1.0.0` |
| `task` | [`task:on-hold`](https://developer.webex.com/docs/webhooks-cc#task-on-hold) | A task is currently on hold since the Agent has placed the Customer on hold. | `task:1.0.0` |
| `task` | [`task:paused`](https://developer.webex.com/docs/webhooks-cc#task-paused) | A task has been paused. | `task:1.0.0` |
| `task` | [`task:resumed`](https://developer.webex.com/docs/webhooks-cc#task-resumed) | A paused task has been resumed. | `task:1.0.0` |
| `task` | [`task:parked`](https://developer.webex.com/docs/webhooks-cc#task-parked) | A task is queued because no agents are currently available to handle the task. | `task:1.0.0` |
| `task` | [`task:conference-transferred`](https://developer.webex.com/docs/webhooks-cc#task-conference-transferred) | A conference is transferred from one Agent to Another Agent. However, the task is still in progress with the Customer. | `task:1.0.0` |
| `task` | [`task:origin-updated`](https://developer.webex.com/docs/webhooks-cc#task-origin-updated) | A task is updated with a new caller origin | `task:1.0.0` |

<a id="task-conference-done"></a>

## Selected section

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
