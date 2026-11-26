---
type: Excerpt
canonical_url: https://developer.webex.com/docs/task-routing-work-items
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Webhook events
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/task-routing-work-items). [Full Markdown](../../../../docs/task-routing-work-items.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before You Begin](003-before-you-begin.md)

## Article introduction

Work Items enable external systems to inject **non-conversational tasks** into Webex Contact Center and can be orchestrated within Webex CC Flow Designer, routed, handled, monitored, and reported alongside other contact center channel interactions.

---

New

**Note:** 
- Work Items do NOT represent live messaging conversations for unsupported channels such as Viber, Instagram, third-party digital channel gateways, etc. A bring-your-own messaging channel should be used for such use cases.
- Use Work Items specifically for backend or offline tasks such as CRM leads, claims, faxes, cases, purchase orders, or other work that needs contact center routing and agent handling without a customer messaging on the other side.

## Selected section

## Webhook events

Use the [Subscriptions API](https://developer.webex.com/webex-contact-center/docs/api/v2/subscriptions) for task lifecycle and Work Item update webhook events.

Important event families for Work Item integrations include:

- `task:new`
- `task:failed`
- `task-message:appended`
- `task-message:append-failed`

Use the [List Event Types API](https://developer.webex.com/webex-contact-center/docs/api/v2/subscriptions/list-event-types) to discover the latest supported event types and resource versions. Use the [Webhooks guide](https://developer.webex.com/docs/webhooks-cc) for detailed event payload documentation.

A `task-message:appended` notification can acknowledge the initial Work Item message or a subsequent metadata update. Its `data.channelProperties` contains message metadata without `message.workItemData`. The full initial Work Item data is available to the flow through the Start node, as described under [Flow Support](https://developer.webex.com/docs/task-routing-work-items#flow-support). Keep your submitted data if your integration needs to correlate the notification with the field values.

Request messages use `type: "work-item-form"`; returned Work Item message metadata uses `type: "work-item"`.

**Representative Work Item `task-message:appended` subscription webhook for the update above:**

```json
{
  "id": "991d52ea-927f-41ff-832b-d8f8601a8fbd",
  "specversion": "1.0",
  "type": "task-message:appended",
  "source": "/com/cisco/wxcc/33333333-3333-4333-8333-333333333333",
  "comciscoorgid": "11111111-1111-4111-8111-111111111111",
  "comciscotimestamp": 1779789109049,
  "datacontenttype": "application/json",
  "data": {
    "taskId": "141897a0-6212-49be-be9d-4823ab1e4dc7",
    "direction": "INBOUND",
    "channelType": "workItem",
    "channel": "ClaimsReview",
    "origin": "crm-lead-10040",
    "destination": "claims-work-items@example.biz",
    "createdTime": 1779789108999,
    "eventDetails": "Appended Work Item data successfully.",
    "channelProperties": {
      "channelType": "workItem",
      "channel": "ClaimsReview",
      "message": {
        "messageId": "44444444-4444-4444-8444-444444444444",
        "aliasId": "991d52ea-927f-41ff-832b-d8f8601a8fbd",
        "direction": "inbound",
        "type": "work-item",
        "timestamp": "2026-05-26T09:51:48.649Z",
        "timestampEpoch": 1779789108649
      },
      "securityComplianceInfo": null
    }
  }
}
```

The following table explains the fields in this successful Work Item notification:

| Field | Description |
| --- | --- |
| `id` | Notification identifier; for a Task Messages update, matches the API response `data.id` |
| `data.taskId` | Work Item task identifier returned by Create Task |
| `data.direction` | Direction of the task; `INBOUND` for Work Items |
| `data.channelType` | `workItem` |
| `data.channel` | Configured Work Item channel name |
| `data.origin` | Source-system identifier supplied in `origin.address` when creating the task |
| `data.destination` | Work Item asset business address supplied in `destination.address` |
| `data.createdTime` | Notification creation time in epoch milliseconds |
| `data.eventDetails` | Status summary, when available |
| `data.channelProperties` | Work Item channel and message metadata; excludes `message.workItemData` |
| `data.channelProperties.message.messageId` | Webex message identifier, separate from the alias and notification ID |
| `data.channelProperties.message.aliasId` | Supplied or generated message alias |
| `data.channelProperties.message.direction` | Lowercase `inbound` |
| `data.channelProperties.message.type` | `work-item` |
| `data.channelProperties.message.timestamp` | Original message time in ISO format |
| `data.channelProperties.message.timestampEpoch` | Original message time as an integer in epoch milliseconds |
| `data.channelProperties.securityComplianceInfo` | Always `null` for Work Items. Work Item data is not scanned for PCI or malware. |

**Representative `task:failed` subscription webhook:**

```json
{
  "id": "8be34eb4-d64f-4552-96cc-c9b6e73063c2",
  "specversion": "1.0",
  "type": "task:failed",
  "source": "/com/cisco/wxcc/33333333-3333-4333-8333-333333333333",
  "comciscoorgid": "11111111-1111-4111-8111-111111111111",
  "comciscotimestamp": "1779785509049",
  "datacontenttype": "application/json",
  "data": {
    "taskId": "141897a0-6212-49be-be9d-4823ab1e4dc7",
    "direction": "inbound",
    "channelType": "workItem",
    "channel": "ClaimsReview",
    "origin": "crm-lead-10040",
    "destination": "claims-work-items@example.biz",
    "createdTime": 1779785508999,
    "reason": "ENTRY_POINT_NOT_FOUND",
    "errorMessage": "The Work Item asset does not resolve to an active entry point.",
    "failureType": "failed"
  }
}
```

**Common failures**

Common cases that can result in `task:failed` include:

- `CHANNEL_ASSET_UNDEFINED`: the destination business address does not resolve to a valid Work Item asset
- `FEATURE_FLAG_DISABLED`: the organization is not enabled for Work Items
- `ENTRY_POINT_NOT_FOUND`: the asset does not resolve to an active entry point
- `ORG_DIGITAL_CONTACT_LIMIT_EXCEEDED`: the organization has reached its active digital contact limit
- `CONVERSATION_ALREADY_OPEN`: an active task already exists for the same origin and destination
- `INVALID_CONTENT`: Work Item content validation failed, such as a missing required schema field
- `INTERNAL_ERROR`: an unexpected failure prevented task creation

Some validation or access failures are returned directly in the HTTP response before acceptance. They do not necessarily produce a `task:failed` event.

**Representative `task-message:append-failed` subscription webhook for a request whose channel does not match the task:**

```json
{
  "id": "64ab4f4a-5c93-4339-b325-3878f289a88f",
  "specversion": "1.0",
  "type": "task-message:append-failed",
  "source": "/com/cisco/wxcc/33333333-3333-4333-8333-333333333333",
  "comciscoorgid": "11111111-1111-4111-8111-111111111111",
  "comciscotimestamp": 1779789109049,
  "datacontenttype": "application/json",
  "data": {
    "taskId": "141897a0-6212-49be-be9d-4823ab1e4dc7",
    "direction": "INBOUND",
    "channelType": "workItem",
    "channel": "ClaimsReview",
    "origin": "crm-lead-10040",
    "destination": "claims-work-items@example.biz",
    "createdTime": 1779789108999,
    "reason": "INVALID_CONTENT",
    "errorMessage": "channelProperties.channel must match the channel specified in the Create Task request."
  }
}
```

Failure notifications include `data.reason` for the failure category and `data.errorMessage` for its explanation.

`task-message:append-failed` contains error metadata without `channelProperties`; use its `id` and `data.taskId` for correlation. For task-message notifications, `data.createdTime` is the notification creation time. Message metadata can contain both an ISO `timestamp` and its epoch-millisecond `timestampEpoch`.

In the task-message notifications shown here, `data.direction` is `INBOUND` and nested `message.direction` is lowercase `inbound`. In the `task:failed` example, `data.direction` is lowercase `inbound`.
