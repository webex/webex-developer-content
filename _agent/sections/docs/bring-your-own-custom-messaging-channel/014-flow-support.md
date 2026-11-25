---
type: Excerpt
canonical_url: https://developer.webex.com/docs/bring-your-own-custom-messaging-channel
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Flow Support
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/bring-your-own-custom-messaging-channel). [Full Markdown](../../../../docs/bring-your-own-custom-messaging-channel.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before You Begin](003-before-you-begin.md) [Authentication For Custom Messaging Integrations](004-authentication-for-custom-messaging-integrations.md) [Attachment URL Requirements](011-attachment-url-requirements.md)

## Article introduction

Connect an external messaging channel to Webex Contact Center through middleware that uses the Custom Messaging APIs.

## Selected section

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
