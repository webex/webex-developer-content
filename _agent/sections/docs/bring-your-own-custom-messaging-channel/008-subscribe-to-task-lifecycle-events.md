---
type: Excerpt
canonical_url: https://developer.webex.com/docs/bring-your-own-custom-messaging-channel
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
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

Representative inbound `task-message:appended` subscription webhook:

```json
{
  "id": "4c2c4890-8a36-4dcc-9702-4c3a4aa1dc51",
  "specversion": "1.0",
  "type": "task-message:appended",
  "source": "/com/cisco/wxcc/ed9357d0-3f5d-4c6a-a4fd-111111111111",
  "comciscoorgid": "cb5901fb-ab66-4377-a7bc-5f0b21896952",
  "comciscotimestamp": 1779785508649,
  "datacontenttype": "application/json",
  "data": {
    "taskId": "044ea619-a0ad-41a3-9ed9-c2563a9bd6b7",
    "direction": "INBOUND",
    "messageDirection": "INBOUND",
    "channelType": "customMessaging",
    "channel": "my-custom-channel",
    "origin": "customer@example.com",
    "destination": "support@channel.biz",
    "createdTime": 1779785508649,
    "eventDetails": "Appended Message to chat successfully.",
    "channelParams": {
      "type": "text-with-attachments",
      "message": {
        "aliasId": "90a896bc-5eb5-4d15-8e11-f62e99751c21",
        "text": "I have more details to share about my order. Please see the attached invoice.",
        "timestamp": 1779785508649,
        "attachments": [
          {
            "fileName": "invoice.pdf",
            "mimeType": "application/pdf",
            "fileUrl": "https://cdn.partner.example.com/files/invoice.pdf"
          }
        ]
      }
    },
    "reason": null,
    "errorMessage": null
  }
}
```

Representative `task:failed` subscription webhook:

```json
{
  "id": "8be34eb4-d64f-4552-96cc-c9b6e73063c2",
  "specversion": "1.0",
  "type": "task:failed",
  "source": "/com/cisco/wxcc/ed9357d0-3f5d-4c6a-a4fd-222222222222",
  "comciscoorgid": "cb5901fb-ab66-4377-a7bc-5f0b21896952",
  "comciscotimestamp": 1779785508649,
  "datacontenttype": "application/json",
  "data": {
    "taskId": "044ea619-a0ad-41a3-9ed9-c2563a9bd6b7",
    "origin": "customer@example.com",
    "destination": "support@channel.biz",
    "direction": "INBOUND",
    "channel": "my-custom-channel",
    "channelType": "customMessaging",
    "mediaMgr": "digitalmm",
    "reason": "CONVERSATION_ALREADY_OPEN",
    "errorMessage": "Conversation is already open with task id ab4ea619-a1ad-33a3-aed9-c2563a9bd6cc",
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
- `CONVERSATION_CREATION_FAILED`: downstream conversation creation failed after the request was accepted
- Validation or policy failures, such as unsupported content, unsupported file types, attachment count limits, or attachment size limits

Representative `task-message:append-failed` subscription webhook:

```json
{
  "id": "64ab4f4a-5c93-4339-b325-3878f289a88f",
  "specversion": "1.0",
  "type": "task-message:append-failed",
  "source": "/com/cisco/wxcc/ed9357d0-3f5d-4c6a-a4fd-333333333333",
  "comciscoorgid": "cb5901fb-ab66-4377-a7bc-5f0b21896952",
  "comciscotimestamp": 1779785508649,
  "datacontenttype": "application/json",
  "data": {
    "taskId": "044ea619-a0ad-41a3-9ed9-c2563a9bd6b7",
    "direction": "INBOUND",
    "messageDirection": "INBOUND",
    "channelType": "customMessaging",
    "channel": "my-custom-channel",
    "origin": "customer@example.com",
    "destination": "support@channel.biz",
    "createdTime": 1779785508649,
    "eventDetails": null,
    "channelParams": null,
    "reason": "INVALID_CONTENT",
    "errorMessage": "The maximum number of attachments allowed is 1."
  }
}
```

Use the following fields to correlate inbound message webhook processing:

- `data.taskId`: task identifier
- `data.channelParams.message.aliasId`: middleware message identifier for `task-message:appended` (when `channelParams` is present)
- `data.messageDirection`: direction of the appended message
- `id`: webhook event identifier
