---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webhooks-cc
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Tasks
- Task Failed
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
