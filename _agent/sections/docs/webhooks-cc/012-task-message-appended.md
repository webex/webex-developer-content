---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webhooks-cc
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
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
