---
type: Excerpt
canonical_url: https://developer.webex.com/docs/bring-your-own-custom-messaging-channel
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Subscribe To Task Lifecycle Events
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/bring-your-own-custom-messaging-channel). [Full Markdown](../../../../docs/bring-your-own-custom-messaging-channel.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before You Begin](003-before-you-begin.md) [Authentication For Custom Messaging Integrations](004-authentication-for-custom-messaging-integrations.md) [Attachment URL Requirements](011-attachment-url-requirements.md)

## Article introduction

Connect an external messaging channel to Webex Contact Center through middleware that uses the Custom Messaging APIs.

## Selected section

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
