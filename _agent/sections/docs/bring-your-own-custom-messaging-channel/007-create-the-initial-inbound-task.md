---
type: Excerpt
canonical_url: https://developer.webex.com/docs/bring-your-own-custom-messaging-channel
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
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

Example request:

```json
{
  "origin": {
    "id": "customer@example.com",
    "name": "Customer Name"
  },
  "destination": {
    "id": "support@channel.biz",
    "type": "businessAddress"
  },
  "channelType": "customMessaging",
  "channel": "my-custom-channel",
  "globalVariables": {
    "customerTier": "gold"
  },
  "channelParams": {
    "type": "text-with-attachments",
    "message": {
      "aliasId": "90a896bc-5eb5-4d15-8e11-f62e99751c21",
      "text": "Hello, I need help with my order. Please see the attached screenshot.",
      "attachments": [
        {
          "fileName": "order-screenshot.png",
          "mimeType": "image/png",
          "fileUrl": "https://cdn.partner.example.com/files/order-screenshot.png"
        }
      ],
      "timestamp": 1779785508649
    }
  }
}
```

Important request fields:

| Parameter | Description | Mandatory |
| --- | --- | --- |
| `origin.id` | Middleware-managed customer identifier | Yes |
| `destination.id` | Business address configured on the asset | Yes |
| `channelType` | Must be `customMessaging` | Yes |
| `channel` | Configured Custom Messaging channel name | Yes |
| `channelParams.type` | Message type, currently `text` or `text-with-attachments` | Yes |
| `channelParams.message.aliasId` | Middleware message identifier | Yes |
| `channelParams.message.text` | Customer message text | Yes |
| `channelParams.message.attachments` | Attachment list for `text-with-attachments` | Conditional |
| `channelParams.message.attachments[].fileName` | Middleware-provided file name | Conditional |
| `channelParams.message.attachments[].mimeType` | Attachment media type | Conditional |
| `channelParams.message.attachments[].fileUrl` | HTTPS URL that the platform can retrieve | Conditional |
| `channelParams.message.timestamp` | Customer message timestamp in epoch milliseconds | Yes |

Message type validation checks from the current routing model:

- `text`: Requires non-empty `text`. Attachments are not supported.
- `text-with-attachments`: Includes `text` and `attachments`. The `attachments` field must be present. Empty text is accepted when attachment content is present. Each attachment entry requires `fileName`, `mimeType`, and HTTPS `fileUrl`.

The guide shows one representative Custom Messaging example. For the full set of supported request combinations and validation rules, refer to the [Create Task API](https://developer.webex.com/webex-contact-center/docs/api/v1/tasks-call-control/create-task).

Example response:

```json
{
  "meta": {
    "orgId": "cb5901fb-ab66-4377-a7bc-5f0b21896952"
  },
  "data": {
    "id": "044ea619-a0ad-41a3-9ed9-c2563a9bd6b7"
  }
}
```

Use `data.id` as the created task identifier. The middleware application should retain this value for subsequent Task Messages API calls and to correlate later task lifecycle subscription webhooks for the interaction.

A `201 Created` response acknowledges that the Create Task request was accepted, but it does not guarantee that the task was fully created successfully. Use `task:new` as the success acknowledgement and `task:failed` as the failure acknowledgement.
