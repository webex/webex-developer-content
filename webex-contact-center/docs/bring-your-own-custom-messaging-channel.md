---
type: Guide
title: Bring Your Own Custom Messaging Channel
display_title: Bring Your Own Custom Messaging Channel
canonical_url: https://developer.webex.com/docs/bring-your-own-custom-messaging-channel
content_type: documentation
product_group:
- webex-contact-center
categories:
- webex-contact-center
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/bring-your-own-custom-messaging-channel)

Connect an external messaging channel to Webex Contact Center through middleware that uses the Custom Messaging APIs.

## Overview

New

In this model:

- A middleware application owns the external messaging channel integration.
- Webex Contact Center owns the contact-center task lifecycle.
- Administrators configure the messaging channel, asset, webhook target, entry point, and flow.
- The middleware application uses public APIs to create tasks and append inbound messages, receives outbound messages through the configured webhook, subscribes to task lifecycle events, and retrieves transcripts.

## Responsibilities

Use this model when your middleware application is responsible for receiving inbound messages from the external messaging channel, forwarding them to Webex Contact Center, and delivering outbound messages from Webex Contact Center back to the end customer.

The middleware application is responsible for:

- Hosting the channel integration
- Obtaining and refreshing OAuth tokens
- Calling the Create Task API for the initial inbound message
- Calling the Task Messages API for subsequent inbound messages
- Processing outbound webhooks received from the asset-level webhook URL
- Subscribing to task lifecycle and inbound message subscription webhooks

Webex Contact Center is responsible for:

- Validating and routing Custom Messaging interactions
- Running the configured flow
- Presenting the conversation to agents
- Generating task lifecycle and task message webhook events
- Storing transcripts for later retrieval

## Before You Begin

Before integrating, ensure that the administrator has configured the following in Control Hub:

- A `Custom Messaging` channel with:
  - Messaging policies for text and attachments
- A `Custom Messaging` asset with:
  - Business address
  - Webhook URL
  - Webhook secret
- A `Custom Messaging` entry point mapped to a `Custom Messaging` flow
- Other Contact Center routing objects required for the interaction, such as queues, teams, and multimedia profiles

## Authentication For Custom Messaging Integrations

- For the middleware application to call the Tasks APIs, you must use a [Service App](https://developer.webex.com/docs/service-apps).
- For scope definitions, refer to [Integration Scopes](https://developer.webex.com/docs/integration-scopes).
- The general [Authentication guide](https://developer.webex.com/docs/authentication) explains token acquisition and token refresh behavior.

### Create And Authorize A Service App

1. Sign in to the developer portal and create a new Service App.
1. Capture the client secret when it is first shown. After the app is submitted for authorization, regenerate the secret if it was not saved.
1. Assign the required scopes:
   - `cjp:task_write`
   - `cjp:task_read`
1. Ask the administrator to authorize the Service App in Control Hub under **Apps**.
1. After authorization, return to the Service App in the developer portal, select the authorized organization, provide the client secret, and generate the access token.

Use the resulting access token when calling the Create Task API and the Task Messages API.

For this integration pattern, ensure that:

- The Service App is authorized for the organization
- The access token includes `cjp:task_write` for Create Task and Task Messages
- The access token includes `cjp:task_read` when task read access is required

### Refresh Tokens

For long-running access, retain the refresh token and use the standard OAuth refresh flow described in the [Authentication guide](https://developer.webex.com/docs/authentication#using-the-refresh-token) before the current access token expires.

For server-to-server integrations, store the client secret, access token, and refresh token securely, and rotate or regenerate credentials according to your organization's security practices.

## Messaging Policy Behavior

Messaging policies are configured on the Custom Messaging channel in Control Hub under Contact Center > Channels & Assets > Channels > Custom Messaging. These policies control:

- Maximum message characters
- Whether attachments are allowed
- Maximum number of attachments
- Maximum total attachment size
- Maximum single attachment size
- Allowed file types

Message text and attachments must comply with your custom channel’s configured limits for text length, attachment count, allowed file types and file sizes. Applicable security policies also apply. The API enforces a maximum of 20,000 text characters and five attachments per message; lower configured limits take precedence.

If an inbound message violates the configured channel policy, the entire message is rejected rather than partially accepted. Attachment drops during PCI or malware scanning are handled separately, as described in [Security, PCI, And Malware Handling](#security-pci-and-malware-handling).

If administrators update the messaging policy, inbound middleware traffic starts using the updated policy almost immediately after the configuration change is applied. For outbound agent messaging, the updated policy is applied after the next relevant desktop reload or session refresh.

## Subscribe Before Sending Traffic

Before using the Create Task API and the Task Messages API, configure subscription webhooks for the task and task-message events that your middleware application needs to process.

At a minimum, subscribe to:

- `task:failed`
- `task-message:appended`
- `task-message:append-failed`

It is also recommended to subscribe to `task:new` and any other task lifecycle events your implementation needs.

Use the [Subscriptions API](https://developer.webex.com/webex-contact-center/docs/api/v1/subscriptions) to register the subscription, and refer to the [Webhooks guide](https://developer.webex.com/docs/webhooks-cc) for payload details and correlation behavior.

## Create The Initial Inbound Task

Use the [Create Task API](https://developer.webex.com/webex-contact-center/docs/api/v1/tasks-call-control/create-task) to create the initial Custom Messaging task.

For Custom Messaging, Create Task supports inbound task creation only. Outbound messages are sent later by flows or agents and are delivered to the middleware application through the configured webhook.

Send the request to `POST /v2/tasks` using the following request body.

Example request:

```json
{
  "origin": {
    "address": "customer@example.com",
    "type": "customerAddress",
    "name": "Customer Name"
  },
  "destination": {
    "address": "support@channel.biz",
    "type": "businessAddress"
  },
  "globalVariables": {
    "customerTier": "gold"
  },
  "channelProperties": {
    "channelType": "customMessaging",
    "channel": "my-custom-channel",
    "message": {
      "type": "text-with-attachments",
      "direction": "inbound",
      "aliasId": "80a896bc-5eb5-4d15-8e11-f62e99751c21",
      "text": "Hello, I need help with my order. Please see the attached screenshot.",
      "attachments": [
        {
          "fileName": "order-screenshot.png",
          "mimeType": "image/png",
          "url": "https://cdn.partner.example.com/files/order-screenshot.png"
        }
      ],
      "timestampEpoch": 1779785508649
    }
  }
}
```

Important request fields:

| Parameter | Description | Mandatory |
| --- | --- | --- |
| `origin.address` | Middleware-managed customer address or identifier | Yes |
| `origin.type` | Must be `customerAddress` | Yes |
| `origin.name` | Customer display name | No |
| `destination.address` | Business address configured on the asset | Yes |
| `destination.type` | Must be `businessAddress` | Yes |
| `channelProperties` | Channel details and initial message, described below | Yes |
| `globalVariables` | Global variables for the interaction | No |
| `flowSettings` | Flow settings supported by the Create Task API | No |

Fields inside `channelProperties` (for example, `message.type` means `channelProperties.message.type`):

| Field | Description | Mandatory |
| --- | --- | --- |
| `channelType` | Must be `customMessaging` | Yes |
| `channel` | Configured Custom Messaging channel name | Yes |
| `message.type` | `text` or `text-with-attachments` | Yes |
| `message.direction` | Must be lowercase `inbound` | Yes |
| `message.aliasId` | Middleware message identifier; a supplied value need not be a UUID and supports up to 200 characters | No |
| `message.text` | Customer message text, supplied as a string; see the rules below | Yes |
| `message.attachments` | Attachment array required for `text-with-attachments`; omit for `text` | Conditional |
| `message.attachments[].fileName` | Nonempty file name for each attachment | Conditional |
| `message.attachments[].mimeType` | Attachment media type when supplied | No |
| `message.attachments[].url` | HTTPS URL that Webex Contact Center can retrieve; maximum 2,000 characters | Conditional |
| `message.timestampEpoch` | Customer message time as an integer in epoch milliseconds | Yes |

The following message rules also apply to subsequent inbound messages sent through the Task Messages API:

- For `type: "text"`, `text` must contain non-whitespace characters. Omit `attachments`; a supplied array, including `[]`, is rejected. An explicit `attachments: null` is treated like omission.
- For `type: "text-with-attachments"`, `text` is required as a string and `attachments` is required as an array. Text may be empty (`""`) when at least one attachment is supplied. Blank text with an empty attachment array is rejected. Nonblank text with `attachments: []` is accepted.
- For an attachment-only inbound message, use `type: "text-with-attachments"`, `text: ""` and a nonempty attachment array. Webex Contact Center supplies the fallback text `Here are your attachments`.
- Each attachment requires `fileName` and HTTPS `url`. `mimeType` is optional; if supplied, it must be a string or null. Attachment content and configured file policies are still validated.
- `aliasId` is optional. If it is omitted, null or empty, Webex Contact Center generates a message alias. See the correlation guidance under [Append Subsequent Inbound Messages](#append-subsequent-inbound-messages).
- `timestampEpoch` is required. Use an integer in epoch milliseconds, such as the result of JavaScript `Date.now()`; do not supply an ISO timestamp or epoch seconds in this input field.

The Create Task API applies a limit to the complete request body, with a configurable default of 900,000 bytes. A request that exceeds the configured limit is rejected with HTTP 413.

The guide shows one representative Custom Messaging example. For the full set of supported request combinations and validation rules, refer to the [Create Task API](https://developer.webex.com/webex-contact-center/docs/api/v1/tasks-call-control/create-task).

Example response:

```json
{
  "meta": {
    "orgId": "11111111-1111-4111-8111-111111111111"
  },
  "data": {
    "id": "044ea619-a0ad-41a3-9ed9-c2563a9bd6b7"
  }
}
```

Use `data.id` as the created task identifier. The middleware application should retain this value for subsequent Task Messages API calls and to correlate later task lifecycle subscription webhooks for the interaction.

A `202 Accepted` response acknowledges that the Create Task request was accepted, but it does not guarantee that the task was fully created successfully. Use `task:new` as the success acknowledgement and `task:failed` as the failure acknowledgement.

## Subscribe To Task Lifecycle Events

Use the [Subscriptions API](https://developer.webex.com/webex-contact-center/docs/api/v1/subscriptions) for task lifecycle and inbound task-message webhook events.

Important event families for Custom Messaging integrations include:

- `task:new`
- `task:connect`
- `task:connected`
- `task:ended`
- `task:failed`
- `task-message:appended`
- `task-message:append-failed`

Use the [List Event Types API](https://developer.webex.com/webex-contact-center/docs/api/v1/subscriptions/list-event-types) to discover the latest supported event types and resource versions.

Use the [Webhooks guide](https://developer.webex.com/docs/webhooks-cc) for detailed task and task-message event payload documentation.

Note that subscription-based `task-message:appended` and `task-message:append-failed` describe inbound task message flows. The outbound webhook documented in this guide is asset-configured and is not delivered through the Subscription API.

A successful initial message and a successful subsequent inbound append each produce a `task-message:appended` notification. The initial notification is separate from the task lifecycle event `task:new`. Inbound success notifications contain `channelProperties` with message metadata and security results when available; they omit message text and attachment objects.

Representative inbound `task-message:appended` subscription webhook for a subsequent message:

```json
{
  "id": "90a896bc-5eb5-4d15-8e11-f62e99751c21",
  "specversion": "1.0",
  "type": "task-message:appended",
  "source": "/com/cisco/wxcc/33333333-3333-4333-8333-333333333333",
  "comciscoorgid": "11111111-1111-4111-8111-111111111111",
  "comciscotimestamp": 1779785569049,
  "datacontenttype": "application/json",
  "data": {
    "taskId": "044ea619-a0ad-41a3-9ed9-c2563a9bd6b7",
    "direction": "INBOUND",
    "channelType": "customMessaging",
    "channel": "my-custom-channel",
    "origin": "customer@example.com",
    "destination": "support@channel.biz",
    "createdTime": 1779785568999,
    "eventDetails": "Appended Message to chat successfully.",
    "channelProperties": {
      "channel": "my-custom-channel",
      "channelType": "customMessaging",
      "message": {
        "messageId": "22222222-2222-4222-8222-222222222222",
        "aliasId": "90a896bc-5eb5-4d15-8e11-f62e99751c21",
        "direction": "inbound",
        "type": "text-with-attachments",
        "timestamp": "2026-05-26T08:52:48.649Z",
        "timestampEpoch": 1779785568649
      },
      "securityComplianceInfo": {
        "droppedAttachmentCount": 0,
        "malwareScan": {
          "isCompliant": true,
          "droppedAttachmentCount": 0,
          "validationDone": true
        },
        "pciScan": {
          "isCompliant": true,
          "textRedacted": false,
          "validationDone": true,
          "droppedAttachmentCount": 0
        }
      }
    }
  }
}
```

Representative `task:failed` subscription webhook:

```json
{
  "id": "8be34eb4-d64f-4552-96cc-c9b6e73063c2",
  "specversion": "1.0",
  "type": "task:failed",
  "source": "/com/cisco/wxcc/33333333-3333-4333-8333-333333333333",
  "comciscoorgid": "11111111-1111-4111-8111-111111111111",
  "comciscotimestamp": "1779785508649",
  "datacontenttype": "application/json",
  "data": {
    "taskId": "044ea619-a0ad-41a3-9ed9-c2563a9bd6b7",
    "origin": "customer@example.com",
    "destination": "support@channel.biz",
    "direction": "inbound",
    "channel": "my-custom-channel",
    "channelType": "customMessaging",
    "reason": "CONVERSATION_ALREADY_OPEN",
    "errorMessage": "Active task already exists for the specified origin and destination, cannot create duplicate task. Open task id: ab4ea619-a1ad-43a3-aed9-c2563a9bd6cc.",
    "failureType": "failed",
    "createdTime": 1779785508649
  }
}
```

Common cases that can result in `task:failed` include:

- `CONVERSATION_ALREADY_OPEN`: a conversation is already active for the same customer and business address
- `CHANNEL_ASSET_UNDEFINED`: the destination business address does not resolve to a valid Custom Messaging asset
- `FEATURE_FLAG_DISABLED`: the organization is not enabled for Custom Messaging
- `ENTRY_POINT_NOT_FOUND`: the asset does not resolve to an active entry point
- `ORG_DIGITAL_CONTACT_LIMIT_EXCEEDED`: the organization has reached its active digital contact limit
- `INVALID_CONTENT`: message validation or policy failed, such as unsupported content, unsupported file types, attachment count limits, or attachment size limits
- `INTERNAL_ERROR`: an unexpected failure prevented task creation

Some validation or access failures are returned directly in the HTTP response before a task request is accepted. They do not necessarily produce a `task:failed` event.

Representative `task-message:append-failed` subscription webhook for a request that exceeds the configured attachment count:

```json
{
  "id": "64ab4f4a-5c93-4339-b325-3878f289a88f",
  "specversion": "1.0",
  "type": "task-message:append-failed",
  "source": "/com/cisco/wxcc/33333333-3333-4333-8333-333333333333",
  "comciscoorgid": "11111111-1111-4111-8111-111111111111",
  "comciscotimestamp": 1779785569049,
  "datacontenttype": "application/json",
  "data": {
    "taskId": "044ea619-a0ad-41a3-9ed9-c2563a9bd6b7",
    "direction": "INBOUND",
    "channelType": "customMessaging",
    "channel": "my-custom-channel",
    "origin": "customer@example.com",
    "destination": "support@channel.biz",
    "createdTime": 1779785568999,
    "reason": "INVALID_CONTENT",
    "errorMessage": "The maximum number of attachments allowed is 1."
  }
}
```

Use the following fields to correlate inbound message webhook processing:

- `data.taskId`: task identifier
- `id`: UUID identifying the notification; for an ordinary append, correlate it with the Task Messages response `data.id`
- `data.channelProperties.message.aliasId`: the supplied or generated message alias, when properties are present
- `data.channelProperties.message.messageId`: Webex message identifier, separate from the alias and notification ID
- `data.direction`: direction of the task
- `data.channelProperties.message.direction`: direction of the message, when properties are present

For the task-message notifications shown here, `data.direction` is `INBOUND`. Nested message direction uses lowercase `inbound` for customer messages and `outbound` for agent or Flow messages. An outbound reply does not change the task direction.

`task-message:append-failed` contains error metadata without `channelProperties`; use its `id` and `data.taskId` for correlation. For inbound task-message success and failure notifications, `data.createdTime` is the notification creation time. Use `message.timestampEpoch` for the original message time when message metadata is present. Returned messages can contain both an ISO `timestamp` and its epoch-millisecond `timestampEpoch`.

## Append Subsequent Inbound Messages

Use the [Task Messages API](https://developer.webex.com/webex-contact-center/docs/api/v1/tasks-call-control/append-task-message) to append subsequent inbound customer messages to the same task.

Send the request to `POST /v2/tasks/{taskId}/messages`, using the task ID returned by Create Task. Include the channel type, channel name and message under `channelProperties`, as shown below. The task ID in the URL identifies the task receiving the message.

Example request:

```json
{
  "channelProperties": {
    "channelType": "customMessaging",
    "channel": "my-custom-channel",
    "message": {
      "type": "text-with-attachments",
      "direction": "inbound",
      "aliasId": "90a896bc-5eb5-4d15-8e11-f62e99751c21",
      "text": "I have more details to share. Please see the attached invoice.",
      "attachments": [
        {
          "fileName": "invoice.pdf",
          "mimeType": "application/pdf",
          "url": "https://cdn.partner.example.com/files/invoice.pdf"
        }
      ],
      "timestampEpoch": 1779785568649
    }
  }
}
```

Example response:

```json
{
  "meta": {
    "orgId": "11111111-1111-4111-8111-111111111111"
  },
  "data": {
    "id": "90a896bc-5eb5-4d15-8e11-f62e99751c21"
  }
}
```

A `202 Accepted` response acknowledges submission, not completion of the append. Use `data.id` to correlate the later `task-message:appended` or `task-message:append-failed` notification. Unlike the Create Task response, this `data.id` identifies the append event, not the task.

The following table shows how the `message.aliasId` supplied in a Task Messages request affects the response and notification identifiers. It also shows whether the alias in a successful notification is preserved or generated.

| Request `message.aliasId` | Task Messages response `data.id` and subsequent notification `id` | Successful notification `message.aliasId` |
| --- | --- | --- |
| UUID string | The supplied UUID | The supplied alias |
| Non-UUID string, such as `partner-message-002` | A separately generated UUID | The supplied alias |
| Omitted, null or empty | A separately generated UUID | A generated message alias |

Do not assume that the notification `id`, `message.aliasId` and `message.messageId` always have the same value.

After a successful append, Webex Contact Center publishes the inbound `task-message:appended` subscription webhook for the same message, and the detailed event payload is documented in [Webhook Event Details](https://developer.webex.com/docs/webhooks-cc).

Important request fields inside `channelProperties` (for example, `message.type` means `channelProperties.message.type`):

| Field | Description | Mandatory |
| --- | --- | --- |
| `channelType` | Must be `customMessaging`, matching the task created earlier | Yes |
| `channel` | Channel specified in the Create Task request | Yes |
| `message.type` | `text` or `text-with-attachments` | Yes |
| `message.direction` | Must be lowercase `inbound` | Yes |
| `message.aliasId` | Optional middleware message identifier, up to 200 characters | No |
| `message.text` | Customer message text as a string | Yes |
| `message.attachments` | Attachment array required for `text-with-attachments`; omit for `text` | Conditional |
| `message.attachments[].fileName` | Nonempty file name for each attachment | Conditional |
| `message.attachments[].mimeType` | Attachment media type when supplied | No |
| `message.attachments[].url` | Retrievable HTTPS attachment URL; maximum 2,000 characters | Conditional |
| `message.timestampEpoch` | Customer message time as an integer in epoch milliseconds | Yes |

The message and attachment rules under [Create The Initial Inbound Task](#create-the-initial-inbound-task) also apply here. The compact UTF-8 representation of `channelProperties` must not exceed 900,000 bytes, including any fallback text added for an attachment-only message. This measures the JSON object, not the downloaded attachment contents.

The channel type and channel must match those used to create the task. A mismatch can be detected after HTTP acceptance and reported through `task-message:append-failed` with reason `INVALID_CONTENT`.

Common inbound append failure categories surfaced through `task-message:append-failed` are shown below, and the detailed event payload is documented in [Webhook Event Details](https://developer.webex.com/docs/webhooks-cc):

| Failure reason | Typical meaning | Typical next step |
| --- | --- | --- |
| `INVALID_CONTENT` | The payload violates message policy or validation rules, or its channel/channel type does not match the task. | Correct the payload to match the channel used in Create Task and its messaging policies, then retry. |
| `NOT_FOUND` | The referenced task context could not be found. | Verify the task identifier before retrying. |
| `INTERNAL_ERROR` | The platform could not complete the append because of an unexpected internal failure. | Investigate the related failure event and retry. |

### Retry Guidance

Assign a UUID to `channelProperties.message.aliasId` for each logical message and reuse that UUID if the same request needs to be retried. Use a different UUID for each new message. If you retry with the same UUID `aliasId`, the platform reuses that UUID as the API response `data.id` and the corresponding notification `id`. If `aliasId` is omitted, null, empty or not a UUID, the platform generates a new event ID for every request, including retries.

After `202 Accepted`, wait for the matching `task-message:appended` or `task-message:append-failed` notification before deciding whether to retry.

## Receive Outbound Partner Webhooks

After the task is created, the associated flow can send outbound messages to the customer. After the task is connected to an agent, the agent can also send outbound messages. All outbound Custom Messaging messages are delivered to the middleware application through the asset-level webhook URL configured on the Control Hub asset.

Outbound webhooks use `data.channelProperties` and contain the message content, accepted attachments and security results when available. For an inbound task, `data.direction` remains `INBOUND` while `data.channelProperties.message.direction` is `outbound`.

Representative system-sent (flow-sent) outbound `task-message:appended` webhook:

```json
{
  "id": "01de1010-a89c-4f3f-9dc1-9497164d3268",
  "specversion": "1.0",
  "type": "task-message:appended",
  "source": "/com/cisco/wxcc/33333333-3333-4333-8333-333333333333",
  "comciscoorgid": "11111111-1111-4111-8111-111111111111",
  "comciscotimestamp": 1779785518899,
  "datacontenttype": "application/json",
  "data": {
    "taskId": "044ea619-a0ad-41a3-9ed9-c2563a9bd6b7",
    "origin": "customer@example.com",
    "destination": "support@channel.biz",
    "senderType": "system",
    "channelType": "customMessaging",
    "channel": "my-custom-channel",
    "createdTime": 1779785518649,
    "direction": "INBOUND",
    "channelProperties": {
      "channelType": "customMessaging",
      "channel": "my-custom-channel",
      "message": {
        "messageId": "44444444-4444-4444-8444-444444444444",
        "aliasId": "4690d7d9-b1a7-4e5b-9568-ca867a26eb49",
        "direction": "outbound",
        "type": "text",
        "text": "Thanks for contacting support. Please share your order number so we can help further.",
        "attachments": [],
        "timestamp": "2026-05-26T08:51:58.649Z",
        "timestampEpoch": 1779785518649
      },
      "securityComplianceInfo": {
        "droppedAttachmentCount": 0,
        "malwareScan": {
          "isCompliant": true,
          "droppedAttachmentCount": 0,
          "validationDone": false
        },
        "pciScan": {
          "isCompliant": true,
          "textRedacted": false,
          "validationDone": true,
          "droppedAttachmentCount": 0
        }
      }
    }
  }
}
```

Representative agent-sent outbound `task-message:appended` webhook:

```json
{
  "id": "11de1010-a89c-4f3f-9dc1-9497164d3268",
  "specversion": "1.0",
  "type": "task-message:appended",
  "source": "/com/cisco/wxcc/33333333-3333-4333-8333-333333333333",
  "comciscoorgid": "11111111-1111-4111-8111-111111111111",
  "comciscotimestamp": 1779785588899,
  "datacontenttype": "application/json",
  "data": {
    "taskId": "044ea619-a0ad-41a3-9ed9-c2563a9bd6b7",
    "origin": "customer@example.com",
    "destination": "support@channel.biz",
    "senderType": "agent",
    "senderId": "5f2ecb3f-1a83-41a9-9b70-c3f8b53b25a0",
    "channelType": "customMessaging",
    "channel": "my-custom-channel",
    "createdTime": 1779785588649,
    "direction": "INBOUND",
    "channelProperties": {
      "channelType": "customMessaging",
      "channel": "my-custom-channel",
      "message": {
        "messageId": "55555555-5555-4555-8555-555555555555",
        "aliasId": "5690d7d9-b1a7-4e5b-9568-ca867a26eb49",
        "direction": "outbound",
        "type": "text",
        "text": "Hello, I am reviewing your request now. I will update you in a moment.",
        "attachments": [],
        "timestamp": "2026-05-26T08:53:08.649Z",
        "timestampEpoch": 1779785588649
      },
      "securityComplianceInfo": {
        "droppedAttachmentCount": 0,
        "malwareScan": {
          "isCompliant": true,
          "droppedAttachmentCount": 0,
          "validationDone": true
        },
        "pciScan": {
          "isCompliant": true,
          "textRedacted": false,
          "validationDone": true,
          "droppedAttachmentCount": 0
        }
      }
    }
  }
}
```

Representative agent-sent outbound `task-message:appended` webhook with attachments and attachment encryption disabled:

```json
{
  "id": "13cfff3d-8f88-4a49-90b9-9d49410abc54",
  "specversion": "1.0",
  "type": "task-message:appended",
  "source": "/com/cisco/wxcc/33333333-3333-4333-8333-333333333333",
  "comciscoorgid": "11111111-1111-4111-8111-111111111111",
  "comciscotimestamp": 1779785608899,
  "datacontenttype": "application/json",
  "data": {
    "taskId": "044ea619-a0ad-41a3-9ed9-c2563a9bd6b7",
    "origin": "customer@example.com",
    "destination": "support@channel.biz",
    "senderType": "agent",
    "senderId": "5f2ecb3f-1a83-41a9-9b70-c3f8b53b25a0",
    "channelType": "customMessaging",
    "channel": "my-custom-channel",
    "createdTime": 1779785608649,
    "direction": "INBOUND",
    "channelProperties": {
      "channelType": "customMessaging",
      "channel": "my-custom-channel",
      "message": {
        "messageId": "88888888-8888-4888-8888-888888888888",
        "aliasId": "e5474344-4cab-4f9b-920e-1890117f9c10",
        "direction": "outbound",
        "type": "text-with-attachments",
        "text": "I am sharing the requested document.",
        "attachments": [
          {
            "url": "https://attachment-api.example.com/files/order-details.pdf",
            "mimeType": "application/pdf",
            "fileName": "order-details.pdf",
            "encrypted": false,
            "fileSize": 4096,
            "dropped": false
          }
        ],
        "timestamp": "2026-05-26T08:53:28.649Z",
        "timestampEpoch": 1779785608649
      },
      "securityComplianceInfo": {
        "droppedAttachmentCount": 0,
        "malwareScan": {
          "isCompliant": true,
          "droppedAttachmentCount": 0,
          "validationDone": true
        },
        "pciScan": {
          "isCompliant": true,
          "textRedacted": false,
          "validationDone": true,
          "droppedAttachmentCount": 0
        }
      }
    }
  }
}
```

Important webhook fields:

| Field | Description |
| --- | --- |
| `id` | UUID identifying this outbound notification; do not treat it as the message ID |
| `data.taskId` | Task identifier for the interaction |
| `data.direction` | Direction of the task; `INBOUND` for these customer-created tasks, including outbound replies |
| `data.senderType` | `system` for flow/system messages or `agent` for agent-sent messages |
| `data.senderId` | Present for agent-sent outbound messages |
| `data.channelProperties.channelType` | `customMessaging` |
| `data.channelProperties.channel` | Configured Custom Messaging channel name |
| `data.channelProperties.message.direction` | `outbound` for delivery to the middleware application |
| `data.channelProperties.message.type` | `text`, `text-with-attachments`, or `attachments` for attachment-only agent messages |
| `data.channelProperties.message.messageId` | Webex message identifier |
| `data.channelProperties.message.aliasId` | Message alias, separate from the Webex message ID and notification ID |
| `data.channelProperties.message.timestamp` | Message time in ISO format |
| `data.channelProperties.message.timestampEpoch` | Message time in epoch milliseconds |
| `data.channelProperties.message.attachments` | Accepted attachment objects when the message includes files |
| `data.channelProperties.message.attachments[].encrypted` | Whether this attachment is encrypted |
| `data.channelProperties.message.attachments[].dropped` | `false` for an accepted attachment |
| `data.channelProperties.message.attachments[].fileSize` | File size in bytes, when supplied |
| `data.channelProperties.securityComplianceInfo` | Security scan and redaction results, when available |

For generic webhook signature, timestamp, replay-protection, and version-header handling, refer to [Using Webhooks](https://developer.webex.com/docs/using-webhooks).

For BYOC outbound `task-message:appended`, the webhook version header is:

```http
X-WebexCC-Webhook-Version: task-message:1.0.0
```

Outbound attachment URLs depend on the organization’s attachment-encryption configuration:

- When attachment encryption is enabled, outbound attachment URLs point to encrypted attachment content
- Otherwise, URLs pointing to plain attachments are returned

Use each attachment’s `encrypted` flag to determine whether decryption is required. For encrypted attachments, the middleware application must use the Webex Decryption SDK before further processing. For the decryption workflow and SDK steps, refer to the `Decrypting Attachments` section in the [Guide for Digital Transcripts](https://developer.webex.com/docs/guide-for-digital-transcripts).

If outbound delivery fails internally, there is no equivalent outbound webhook failure event unless future implementation changes introduce one.

## Attachment URL Requirements

These requirements apply to middleware-provided attachment URLs used by:

- Create Task
- Task Messages
- Flow/system-sent Custom Messaging attachments where the platform must retrieve the file

Requirements:

- Supply the attachment URL in the JSON key `url`; it must use `https` and be at most 2,000 characters long
- The service must be able to download the file directly, without a separate login or Authorization header. A signed or short-lived URL is acceptable if it remains valid until the file is downloaded
- Supply a nonempty `fileName`. `mimeType` is optional; omitting it does not bypass file-type or content validation
- File-type validation uses the URL extension when present. If no usable extension is present, it can use the filename and content type returned by the file server, together with the supplied MIME type when applicable
- If the effective file type is unsupported by the configured channel policy, the message is rejected
- When the configured policy enforces attachment size limits, file size must be determinable from remote metadata such as `Content-Length`; otherwise, the message is rejected

These rules are separate from agent desktop attachment uploads, which follow a different UI-driven validation path.

## Security, PCI, And Malware Handling

Custom Messaging webhooks use the same signature, timestamp, replay-protection, and version-header validation model as other Webex Contact Center webhooks. For the generic validation steps, see [Using Webhooks](https://developer.webex.com/docs/using-webhooks).

For message content handling:

- PCI-sensitive text is masked and processing continues
- For inbound create-task and inbound task-message flows, attachments that fail PCI or malware scanning are dropped while the message continues
- Inbound success payloads can include an `eventDetails` summary; use `channelProperties.securityComplianceInfo` for structured scan and redaction results
- Inbound middleware webhooks contain message metadata and security results without text or attachment objects. Validated content is available to the flow through Start and Receive nodes.
- Outbound middleware webhooks contain the surviving attachments. Dropped filenames and failure details can be reported separately in the security results
- Agent outbound attachment uploads are blocked before send when the file violates the enforced data security policy

`securityComplianceInfo` can include a total `droppedAttachmentCount`, `malwareScan` and `pciScan`. Read `validationDone` together with `isCompliant`; `pciScan.textRedacted` indicates text masking. Scan `files` arrays can identify affected files using `name`, `errorCode` and `errorMsg`. Availability depends on the checks performed.

Representative inbound success notification data indicating that PCI text was masked. The notification omits the text itself:

```json
{
  "data": {
    "taskId": "5bf807cb-8f35-4f40-8261-1e2d05d41123",
    "direction": "INBOUND",
    "channelType": "customMessaging",
    "channel": "my-custom-channel",
    "origin": "customer@example.com",
    "destination": "support@channel.biz",
    "createdTime": 1780295174159,
    "eventDetails": "Chat Created Successfully.",
    "channelProperties": {
      "channel": "my-custom-channel",
      "channelType": "customMessaging",
      "message": {
        "messageId": "66666666-6666-4666-8666-666666666666",
        "aliasId": "cd0857f0-6b07-4e57-b821-9ae04b7f8bc8",
        "direction": "inbound",
        "type": "text-with-attachments",
        "timestamp": "2026-06-01T06:26:13.809Z",
        "timestampEpoch": 1780295173809
      },
      "securityComplianceInfo": {
        "droppedAttachmentCount": 0,
        "malwareScan": {
          "isCompliant": true,
          "droppedAttachmentCount": 0,
          "validationDone": false
        },
        "pciScan": {
          "isCompliant": false,
          "textRedacted": true,
          "validationDone": true,
          "droppedAttachmentCount": 0
        }
      }
    }
  }
}
```

Representative inbound success notification data when malware scanning drops an attachment. The security results identify the dropped file; the notification does not contain attachment objects:

```json
{
  "data": {
    "taskId": "5bf807cb-8f35-4f40-8261-1e2d05d41123",
    "direction": "INBOUND",
    "channelType": "customMessaging",
    "channel": "my-custom-channel",
    "origin": "customer@example.com",
    "destination": "support@channel.biz",
    "createdTime": 1780300207803,
    "eventDetails": "Appended Message to chat successfully. Some attachments were dropped.",
    "channelProperties": {
      "channel": "my-custom-channel",
      "channelType": "customMessaging",
      "message": {
        "messageId": "77777777-7777-4777-8777-777777777777",
        "aliasId": "4a5a6865-feb6-49c3-a966-d493eccd0cf1",
        "direction": "inbound",
        "type": "text-with-attachments",
        "timestamp": "2026-06-01T07:50:07.453Z",
        "timestampEpoch": 1780300207453
      },
      "securityComplianceInfo": {
        "droppedAttachmentCount": 1,
        "malwareScan": {
          "isCompliant": false,
          "droppedAttachmentCount": 1,
          "validationDone": true,
          "files": [
            {
              "name": "blocked-file.pdf",
              "errorCode": "MALWARE_DETECTED",
              "errorMsg": "Malware was detected"
            }
          ]
        },
        "pciScan": {
          "isCompliant": true,
          "textRedacted": false,
          "validationDone": true,
          "droppedAttachmentCount": 0,
          "files": []
        }
      }
    }
  }
}
```

## Error Handling And Recovery

The middleware application should treat `task:failed` and `task-message:append-failed` as the main failure events for create-task and inbound append operations.

Important guidance:

- `task:failed` is the failure event for create-task failures
- `task-message:append-failed` is the failure event for inbound task-message failures
- Representative append-failure reasons include `INVALID_CONTENT`, `INTERNAL_ERROR`, and `NOT_FOUND`
- Handle immediate HTTP errors separately from failures reported after `202 Accepted`; an invalid request rejected before acceptance does not necessarily produce a subscription event
- Correlate append notifications using the Task Messages response `data.id`, rather than assuming a message alias is always the notification ID
- Use the structured `reason` for failure handling. Example error messages are illustrative and can vary with the validation failure

For stuck-contact recovery:

- If the middleware application receives `task:failed` for a `CONVERSATION_ALREADY_OPEN` condition
- If the error message provides the existing task identifier, use it to investigate that task
- Call [End Task](https://developer.webex.com/webex-contact-center/docs/api/v1/tasks-call-control/end-task) only when you have confirmed that the earlier task should be closed.
- Be cautious before ending the earlier task, because it may still be in a valid queued or active state. Only use End Task when you have confirmed that the earlier task is stale and should be closed
- Retry Create Task only after the existing task has been cleaned up, if your workflow requires a retry

## Flow Support

Custom Messaging flows support:

- `Send Custom Message`
- `Receive Message`

`Receive Message` allows the flow to wait for an inbound customer message before the flow continues.

Parse `MediaPayload` for the Start node and Send Custom Message activity, and `ChannelProperties` for the Receive Message activity.

The Start and Receive payloads include validated inbound content; successful inbound `task-message:appended` notifications omit message text and attachment objects.

### Start And Receive Payloads

Start and Receive expose the normalized incoming message envelope, including validated text, accepted attachments, message metadata and security results when available. The following example assumes attachment encryption is disabled and shows a message with one accepted file and one file dropped by malware scanning:

```json
{
  "channel": "my-custom-channel",
  "channelType": "customMessaging",
  "message": {
    "messageId": "77777777-7777-4777-8777-777777777777",
    "aliasId": "4a5a6865-feb6-49c3-a966-d493eccd0cf1",
    "direction": "inbound",
    "type": "text-with-attachments",
    "timestamp": "2026-06-01T07:50:07.453Z",
    "timestampEpoch": 1780300207453,
    "text": "Here is the requested invoice.",
    "attachments": [
      {
        "fileName": "invoice.pdf",
        "mimeType": "application/pdf",
        "url": "https://attachment-api.example.com/files/invoice.pdf",
        "encrypted": false,
        "fileSize": 4096,
        "dropped": false
      }
    ]
  },
  "securityComplianceInfo": {
    "droppedAttachmentCount": 1,
    "malwareScan": {
      "isCompliant": false,
      "droppedAttachmentCount": 1,
      "validationDone": true,
      "files": [
        {
          "name": "blocked-file.pdf",
          "errorCode": "MALWARE_DETECTED",
          "errorMsg": "Malware was detected"
        }
      ]
    },
    "pciScan": {
      "isCompliant": true,
      "textRedacted": false,
      "validationDone": true,
      "droppedAttachmentCount": 0,
      "files": []
    }
  }
}
```

In the Start activity, use Parse settings to extract attributes from the `MediaPayload` object into flow variables. Enter JSON paths relative to that object, such as `$.message.text`; there is no separate MediaPayload field to select in Parse settings.

For BYOC Receive, use Parse settings to extract attributes from the `ChannelProperties` object. Start and Receive use the same relative JSON paths:

| JSON path | Value to extract |
| --- | --- |
| `$.message.text` | Validated incoming text |
| `$.message.attachments` | Accepted attachments, with returned URLs and encryption metadata |
| `$.message.aliasId` | Supplied or generated message alias |
| `$.message.messageId` | Webex message identifier |
| `$.message.timestampEpoch` | Original message time in epoch milliseconds |
| `$.securityComplianceInfo` | Available scan and redaction results |

### Send Result Payload

Send Custom Message returns `MediaPayload`. Use its Parse settings to extract message metadata, delivery receipt and security results. The Send result omits message text and attachment objects; the outbound partner webhook carries that content.

Representative Send `MediaPayload`:

```json
{
  "channel": "my-custom-channel",
  "channelType": "customMessaging",
  "message": {
    "messageId": "99999999-9999-4999-8999-999999999999",
    "aliasId": "a1111111-1111-4111-8111-111111111111",
    "direction": "outbound",
    "type": "text-with-attachments",
    "receiptCode": "delivered",
    "timestamp": "2026-06-01T07:50:17.453Z",
    "timestampEpoch": 1780300217453
  },
  "securityComplianceInfo": {
    "droppedAttachmentCount": 1,
    "malwareScan": {
      "isCompliant": false,
      "droppedAttachmentCount": 1,
      "validationDone": true,
      "files": [
        {
          "name": "blocked-file.pdf",
          "errorCode": "MALWARE_DETECTED",
          "errorMsg": "Malware was detected"
        }
      ]
    },
    "pciScan": {
      "isCompliant": true,
      "textRedacted": false,
      "validationDone": true,
      "droppedAttachmentCount": 0,
      "files": []
    }
  }
}
```

Use paths such as `$.message.receiptCode` and `$.securityComplianceInfo`. Save outgoing text or attachment details in flow variables before Send if later activities need them. Payload fields can be unavailable on failure or timeout; check the activity outcome before using parsed values.

### Configure The Flow

- In Start, parse attributes from the `MediaPayload` object into flow variables
- For Send, parse `MediaPayload`; for BYOC Receive, parse `ChannelProperties`
- Use `url` in attachment objects built in integrations, scripts or variables. The corresponding Flow Designer input is labelled **File URL**
- Configure downstream expressions to use the parsed variables, then validate and publish the flow

Flow debug and runtime outputs include `ErrorCode`, `ErrorMessage` and `TrackingId` for investigating send or receive failures. Use structured security results for scan and redaction decisions. Receive can also provide an optional `Description` summary when available.

## Retrieve Transcripts

Use the [Captures API](https://developer.webex.com/webex-contact-center/docs/api/v1/captures/list-captures) to retrieve post-interaction transcripts for Custom Messaging tasks.

Custom Messaging transcripts are retrieved after transcript generation, subject to retention and capture availability.
