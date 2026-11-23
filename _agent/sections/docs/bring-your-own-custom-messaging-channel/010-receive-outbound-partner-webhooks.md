---
type: Excerpt
canonical_url: https://developer.webex.com/docs/bring-your-own-custom-messaging-channel
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Receive Outbound Partner Webhooks
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/bring-your-own-custom-messaging-channel). [Full Markdown](../../../../docs/bring-your-own-custom-messaging-channel.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before You Begin](003-before-you-begin.md) [Authentication For Custom Messaging Integrations](004-authentication-for-custom-messaging-integrations.md) [Attachment URL Requirements](011-attachment-url-requirements.md)

## Article introduction

Connect an external messaging channel to Webex Contact Center through middleware that uses the Custom Messaging APIs.

## Selected section

## Receive Outbound Partner Webhooks

After the task is created, the associated flow can send outbound messages to the customer. After the task is connected to an agent, the agent can also send outbound messages. All outbound Custom Messaging messages are delivered to the middleware application through the asset-level webhook URL configured on the Control Hub asset.

Representative system-sent (flow-sent) outbound `task-message:appended` webhook:

```json
{
  "id": "01de1010-a89c-4f3f-9dc1-9497164d3268",
  "specversion": "1.0",
  "type": "task-message:appended",
  "source": "/com/cisco/wxcc/15858e1d-5059-45fd-aee1-fc314c42a790",
  "comciscoorgid": "cb5901fb-ab66-4377-a7bc-5f0b21896952",
  "comciscotimestamp": 1779785486332,
  "datacontenttype": "application/json",
  "data": {
    "taskId": "044ea619-a0ad-41a3-9ed9-c2563a9bd6b7",
    "origin": "customer@example.com",
    "destination": "support@channel.biz",
    "messageDirection": "OUTBOUND",
    "senderType": "system",
    "channelType": "customMessaging",
    "channel": "my-custom-channel",
    "channelParams": {
      "type": "text",
      "message": {
        "aliasId": "4690d7d9-b1a7-4e5b-9568-ca867a26eb49",
        "text": "Thanks for contacting support. Please share your order number so we can help further.",
        "timestamp": 1779760284456,
        "attachments": []
      }
    },
    "createdTime": 1779760284456
  }
}
```

Representative agent-sent outbound `task-message:appended` webhook:

```json
{
  "id": "11de1010-a89c-4f3f-9dc1-9497164d3268",
  "specversion": "1.0",
  "type": "task-message:appended",
  "source": "/com/cisco/wxcc/15858e1d-5059-45fd-aee1-fc314c42a790",
  "comciscoorgid": "cb5901fb-ab66-4377-a7bc-5f0b21896952",
  "comciscotimestamp": 1779785586332,
  "datacontenttype": "application/json",
  "data": {
    "taskId": "044ea619-a0ad-41a3-9ed9-c2563a9bd6b7",
    "origin": "customer@example.com",
    "destination": "support@channel.biz",
    "messageDirection": "OUTBOUND",
    "senderType": "agent",
    "senderId": "5f2ecb3f-1a83-41a9-9b70-c3f8b53b25a0",
    "channelType": "customMessaging",
    "channel": "my-custom-channel",
    "channelParams": {
      "type": "text",
      "message": {
        "aliasId": "5690d7d9-b1a7-4e5b-9568-ca867a26eb49",
        "text": "Hello, I am reviewing your request now. I will update you in a moment.",
        "timestamp": 1779785586332,
        "attachments": []
      }
    },
    "createdTime": 1779785586332
  }
}
```

Representative agent-sent outbound `task-message:appended` webhook with attachments:

```json
{
  "id": "13cfff3d-8f88-4a49-90b9-9d49410abc54",
  "specversion": "1.0",
  "type": "task-message:appended",
  "source": "/com/cisco/wxcc/15858e1d-5059-45fd-aee1-fc314c42a790",
  "comciscoorgid": "cb5901fb-ab66-4377-a7bc-5f0b21896952",
  "comciscotimestamp": 1779786678879,
  "datacontenttype": "application/json",
  "data": {
    "taskId": "044ea619-a0ad-41a3-9ed9-c2563a9bd6b7",
    "origin": "customer@example.com",
    "destination": "support@channel.biz",
    "messageDirection": "OUTBOUND",
    "senderType": "agent",
    "senderId": "5f2ecb3f-1a83-41a9-9b70-c3f8b53b25a0",
    "channelType": "customMessaging",
    "channel": "my-custom-channel",
    "channelParams": {
      "type": "text-with-attachments",
      "message": {
        "aliasId": "e5474344-4cab-4f9b-920e-1890117f9c10",
        "text": "I am sharing the requested document.",
        "timestamp": 1779786678831,
        "attachments": [
          {
            "url": "https://attachment-api.example.com/api/v1/attachments/87da5468-9e09-49db-883e-dce1e8d62fac?token=<signed-url-token>",
            "mimeType": "application/pdf",
            "fileName": "order-details.pdf"
          }
        ]
      }
    },
    "createdTime": 1779786678831
  }
}
```

Important webhook fields:

| Field | Description |
| --- | --- |
| `id` | Webhook event identifier |
| `data.taskId` | Task identifier for the interaction |
| `data.messageDirection` | `OUTBOUND` for outbound delivery to the middleware application |
| `data.senderType` | `system` for flow/system messages or `agent` for agent-sent messages |
| `data.senderId` | Present for agent-sent outbound messages |
| `data.channelParams.type` | Outbound message payload type such as `text` or `text-with-attachments` |
| `data.channelParams.message.aliasId` | Message identifier |
| `data.channelParams.message.attachments` | Present when the outbound message includes files |

For generic webhook signature, timestamp, replay-protection, and version-header handling, refer to [Using Webhooks](https://developer.webex.com/docs/using-webhooks).

For BYOC outbound `task-message:appended`, the webhook version header is:

```http
X-WebexCC-Webhook-Version: task-message:1.0.0
```

Outbound attachment URLs depend on the organization’s attachment-encryption configuration:

- When attachment encryption is enabled, outbound attachment URLs point to encrypted attachment content
- Otherwise, URLs pointing to plain attachments are returned

When attachment encryption is enabled, the middleware application must use the Webex Decryption SDK to decrypt those attachments before further processing. For the decryption workflow and SDK steps, refer to the `Decrypting Attachments` section in the [Guide for Digital Transcripts](https://developer.webex.com/docs/guide-for-digital-transcripts).

If outbound delivery fails internally, there is no equivalent outbound webhook failure event unless future implementation changes introduce one.
