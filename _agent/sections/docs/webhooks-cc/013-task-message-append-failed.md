---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webhooks-cc
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Tasks
- Task Message Append Failed
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

The task resource represents a request or demand for work from agents. Concretely, a telephony task is an incoming call. Tasks are not considered complete until all parties have wrapped up, i.e., the customer has terminated communication and the agent has completed any summary/“wrap-up” work. Tasks are most commonly initiated by the customer (inbound), but can also be initiated by an agent (outbound). Task APIs support telephony. Custom Messaging and Work Item integrations use the Create Task API for inbound task creation and the Task Messages API for subsequent messages or metadata updates. See [Custom Messaging](https://developer.webex.com/docs/bring-your-own-custom-messaging-channel) and [Work Items](https://developer.webex.com/docs/task-routing-work-items) for the request formats and integration steps.

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
| `task-message` | [`task-message:appended`](https://developer.webex.com/docs/webhooks-cc#task-message-appended) | An inbound message or Work Item metadata was appended to the task's conversation. | `task-message:1.0.0` |
| `task-message` | [`task-message:append-failed`](https://developer.webex.com/docs/webhooks-cc#task-message-append-failed) | An inbound message or Work Item metadata failed to be appended to the task's conversation. | `task-message:1.0.0` |
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
