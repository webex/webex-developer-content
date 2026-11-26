---
type: Excerpt
canonical_url: https://developer.webex.com/docs/bring-your-own-custom-messaging-channel
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Create The Initial Inbound Task
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/bring-your-own-custom-messaging-channel). [Full Markdown](../../../../docs/bring-your-own-custom-messaging-channel.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before You Begin](003-before-you-begin.md) [Authentication For Custom Messaging Integrations](004-authentication-for-custom-messaging-integrations.md) [Attachment URL Requirements](011-attachment-url-requirements.md)

## Article introduction

Connect an external messaging channel to Webex Contact Center through middleware that uses the Custom Messaging APIs.

## Selected section

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
- `aliasId` is optional. If it is omitted, null or empty, Webex Contact Center generates a message alias. See the correlation guidance under [Append Subsequent Inbound Messages](https://developer.webex.com/docs/bring-your-own-custom-messaging-channel#append-subsequent-inbound-messages).
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
