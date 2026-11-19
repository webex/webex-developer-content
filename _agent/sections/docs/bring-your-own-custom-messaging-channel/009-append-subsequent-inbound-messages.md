---
type: Excerpt
canonical_url: https://developer.webex.com/docs/bring-your-own-custom-messaging-channel
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Append Subsequent Inbound Messages
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/bring-your-own-custom-messaging-channel). [Full Markdown](../../../../docs/bring-your-own-custom-messaging-channel.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before You Begin](003-before-you-begin.md) [Authentication For Custom Messaging Integrations](004-authentication-for-custom-messaging-integrations.md) [Attachment URL Requirements](011-attachment-url-requirements.md)

## Article introduction

Connect an external messaging channel to Webex Contact Center through middleware that uses the Custom Messaging APIs.

## Selected section

## Append Subsequent Inbound Messages

Use the [Task Messages API](https://developer.webex.com/webex-contact-center/docs/api/v1/tasks-call-control/append-task-message) to append subsequent inbound customer messages to the same task.

Example request:

```json
{
  "mediaType": "customMessaging",
  "channelParams": {
    "type": "text-with-attachments",
    "message": {
      "aliasId": "90a896bc-5eb5-4d15-8e11-f62e99751c21",
      "text": "I have more details to share. Please see the attached invoice.",
      "attachments": [
        {
          "fileName": "invoice.pdf",
          "mimeType": "application/pdf",
          "fileUrl": "https://cdn.partner.example.com/files/invoice.pdf"
        }
      ],
      "timestamp": 1779785508649
    }
  }
}
```

Example response:

```json
{
  "meta": {
    "orgId": "cb5901fb-ab66-4377-a7bc-5f0b21896952"
  },
  "data": {
    "id": "90a896bc-5eb5-4d15-8e11-f62e99751c21"
  }
}
```

Use `data.id` as the append event correlation identifier. If request `aliasId` is a valid UUID, the platform reuses that value as the event identifier.

After a successful append, Webex Contact Center publishes the inbound `task-message:appended` subscription webhook for the same message, and the detailed event payload is documented in [Webhook Event Details](https://developer.webex.com/docs/webhooks-cc).

Important request fields:

| Parameter | Description | Mandatory |
| --- | --- | --- |
| `mediaType` | Must be `customMessaging` | Yes |
| `channelParams.type` | Message payload type, such as `text` or `text-with-attachments` | Yes |
| `channelParams.message.aliasId` | Middleware message identifier for correlation | Yes |
| `channelParams.message.text` | Customer message text | Yes |
| `channelParams.message.attachments` | Attachment list used with `text-with-attachments` | Conditional |
| `channelParams.message.attachments[].fileName` | Middleware-provided file name | Conditional |
| `channelParams.message.attachments[].mimeType` | Attachment media type | Conditional |
| `channelParams.message.attachments[].fileUrl` | HTTPS URL that the platform can retrieve | Conditional |
| `channelParams.message.timestamp` | Customer message timestamp in epoch milliseconds | Yes |

Common inbound append failure categories surfaced through `task-message:append-failed` are shown below, and the detailed event payload is documented in [Webhook Event Details](https://developer.webex.com/docs/webhooks-cc):

| Failure reason | Typical meaning | Typical next step |
| --- | --- | --- |
| `INVALID_CONTENT` | The request payload violates message policy or validation rules, such as unsupported content, unsupported file type, too many attachments, or attachment size limits. | Correct the request payload and retry. |
| `NOT_FOUND` | The referenced task context could not be found. | Verify the task identifier before retrying. |
| `INTERNAL_ERROR` | The platform could not complete the append because of an unexpected internal failure. | Investigate the related failure event and retry. |
