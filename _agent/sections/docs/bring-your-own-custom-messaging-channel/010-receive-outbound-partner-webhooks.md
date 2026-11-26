---
type: Excerpt
canonical_url: https://developer.webex.com/docs/bring-your-own-custom-messaging-channel
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
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
