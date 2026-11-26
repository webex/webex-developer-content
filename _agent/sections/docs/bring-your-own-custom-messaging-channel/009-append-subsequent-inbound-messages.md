---
type: Excerpt
canonical_url: https://developer.webex.com/docs/bring-your-own-custom-messaging-channel
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
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

The message and attachment rules under [Create The Initial Inbound Task](https://developer.webex.com/docs/bring-your-own-custom-messaging-channel#create-the-initial-inbound-task) also apply here. The compact UTF-8 representation of `channelProperties` must not exceed 900,000 bytes, including any fallback text added for an attachment-only message. This measures the JSON object, not the downloaded attachment contents.

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
