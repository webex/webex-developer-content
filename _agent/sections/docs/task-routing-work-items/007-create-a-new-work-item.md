---
type: Excerpt
canonical_url: https://developer.webex.com/docs/task-routing-work-items
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Create a new work item
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

## Create a new work item

Use the [Create Task API](https://developer.webex.com/webex-contact-center/docs/api/v1/tasks-call-control/create-task) to create the initial Work Item task.

Send the request to `POST /v2/tasks` using the following request body. This example assumes that the asset schema contains the illustrated fields and that `claimNumber` is required.

**Example request:**

```json
{
  "origin": {
    "address": "crm-lead-10040",
    "name": "Customer Name",
    "type": "customerAddress"
  },
  "destination": {
    "address": "claims-work-items@example.biz",
    "type": "businessAddress"
  },
  "flowSettings": {
    "foo": "bar"
  },
  "globalVariables": {
    "var1": "val1"
  },
  "channelProperties": {
    "channelType": "workItem",
    "channel": "ClaimsReview",
    "message": {
      "aliasId": "51b8f31d-05b2-45f8-b172-63920f2b7d9a",
      "direction": "inbound",
      "type": "work-item-form",
      "workItemData": {
        "customerAccountId": "account-001",
        "customerAccountName": "Customer Name",
        "claimNumber": "CLM-001",
        "priority": "High",
        "claimStatus": "New"
      },
      "timestampEpoch": 1779785508649
    }
  }
}
```

**Important request fields:**

| Parameter | Description | Mandatory |
| --- | --- | --- |
| `origin.address` | Developer-defined customer, case, task or source-system identifier | Yes |
| `origin.type` | Must be `customerAddress` | Yes |
| `origin.name` | Display name associated with the Work Item origin | No |
| `destination.address` | Business address configured on the Work Item asset | Yes |
| `destination.type` | Must be `businessAddress` | Yes |
| `channelProperties` | Work Item channel and message details | Yes |
| `flowSettings` | Optional flow settings, represented as string key/value pairs | No |
| `globalVariables` | Global variables supplied to the task | No |

Fields inside `channelProperties`:

| Field | Description | Mandatory |
| --- | --- | --- |
| `channelType` | Must be `workItem` | Yes |
| `channel` | Configured Work Item channel name | Yes |
| `message.type` | Must be `work-item-form` | Yes |
| `message.direction` | Must be lowercase `inbound` | Yes |
| `message.aliasId` | Developer-provided message reference, up to 200 characters; it need not be a UUID | No |
| `message.workItemData` | Nonempty string key/value object that satisfies the asset schema, including every required field | Yes |
| `message.timestampEpoch` | Message time as an integer in epoch milliseconds | Yes |

If `aliasId` is omitted, null or empty, Webex Contact Center generates a message alias. Use an integer in epoch milliseconds for `timestampEpoch`, such as the result of JavaScript `Date.now()`.

The Create Task API applies a limit to the complete request body, with a configurable default of 900,000 bytes. A request that exceeds the configured limit is rejected with HTTP 413.

For the full set of supported request combinations and validation rules, refer to the [Create Task API](https://developer.webex.com/webex-contact-center/docs/api/v1/tasks-call-control/create-task).

**Example response — `202 Accepted`:**

```json
{
  "meta": {
    "orgId": "11111111-1111-4111-8111-111111111111"
  },
  "data": {
    "id": "141897a0-6212-49be-be9d-4823ab1e4dc7"
  }
}
```

Use `data.id` as the created task identifier. Retain this value for subsequent Task Messages API calls and to correlate later task lifecycle subscription webhooks.

`202 Accepted` acknowledges submission; it does not confirm that the Work Item was created. Monitor the task lifecycle events and `task:failed` for the outcome. A successful initial Work Item message also produces a `task-message:appended` notification.
