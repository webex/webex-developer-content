---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webhooks-cc
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Tasks
- Task Message Appended
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

### Task Message Appended

`task-message:appended`

**Resource Version: task-message:1.0.0**

An event indicating that an inbound message has been successfully appended to a task's conversation. This section documents the subscription webhook for inbound task-message flows. Outbound asset-configured partner webhooks are documented separately in the Bring Your Own Custom Messaging Channel guide.

| Field | Type | Description | Example |
| --- | --- | --- | --- |
| `taskId` | `string` | The ID associated with the task to which the message was appended. | `"888b688e-b74e-4fa6-8260-1e8d0a3523a"` |
| `direction` | `string, optional` | Direction of the overall task. | `"INBOUND"` |
| `messageDirection` | `string` | Direction of the appended message. For this subscription webhook, the common value is `INBOUND`. | `"INBOUND"` |
| `channelType` | `string, optional` | The channel type of the task. | `"customMessaging"` |
| `channel` | `string, optional` | Configured channel name for the task when available. | `"my-custom-channel"` |
| `origin` | `string, optional` | Customer identifier associated with the task when available. | `"customer@example.com"` |
| `destination` | `string, optional` | Business address associated with the task when available. | `"support@channel.biz"` |
| `createdTime` | `integer, optional` | Message creation time in epoch milliseconds. | `1780295173809` |
| `eventDetails` | `string, optional` | Partner-visible status details for successful append processing. | `"Appended Message to chat successfully."` |
| `channelParams` | `object, optional` | Appended message payload. This typically includes the message `type`, nested message `aliasId`, `text`, optional `attachments`, and `timestamp`. | Custom Messaging message payload |
| `reason` | `string, optional` | Usually `null` for success payloads. | `null` |
| `errorMessage` | `string, optional` | Usually `null` for success payloads. | `null` |

<a id="task-message-append-failed"></a>
