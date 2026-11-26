---
type: Excerpt
canonical_url: https://developer.webex.com/docs/task-routing-work-items
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Update Work Item Data
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

## Update Work Item Data

Use the [Task Messages API](https://developer.webex.com/webex-contact-center/docs/api/v1/tasks-call-control/append-task-message) to append a metadata update to an existing Work Item.

Send the request to `POST /v2/tasks/{taskId}/messages`, using the task ID returned by Create Task. The channel type and channel must match those used to create the task. This updates Work Item metadata; it does not send a conversational chat message.

The following example updates `claimStatus`. The required `claimNumber` field from the creation example is unchanged, so it does not need to be repeated.

**Example request:**

```json
{
  "channelProperties": {
    "channelType": "workItem",
    "channel": "ClaimsReview",
    "message": {
      "aliasId": "991d52ea-927f-41ff-832b-d8f8601a8fbd",
      "direction": "inbound",
      "type": "work-item-form",
      "workItemData": {
        "claimStatus": "Approved"
      },
      "timestampEpoch": 1779789108649
    }
  }
}
```

**Example response — `202 Accepted`:**

```json
{
  "meta": {
    "orgId": "11111111-1111-4111-8111-111111111111"
  },
  "data": {
    "id": "991d52ea-927f-41ff-832b-d8f8601a8fbd"
  }
}
```

Use response `data.id` to correlate the request with the later `task-message:appended` or `task-message:append-failed` notification's `id`. This identifier represents the update event, not the task. A `202 Accepted` response acknowledges submission, not completion of the update.

The following table shows how the `message.aliasId` supplied in a Task Messages request affects the response and notification identifiers. It also shows whether the alias in a successful notification is preserved or generated.

| Request `message.aliasId` | Task Messages response `data.id` and subsequent notification `id` | Successful notification `message.aliasId` |
| --- | --- | --- |
| UUID string | The supplied UUID | The supplied alias |
| Non-UUID string, such as `partner-update-002` | A separately generated UUID | The supplied alias |
| Omitted, null or empty | A separately generated UUID | A generated message alias |

Do not assume that the notification `id`, `message.aliasId` and `message.messageId` always have the same value.

After a successful update, Webex Contact Center publishes the inbound `task-message:appended` subscription webhook for the same Work Item update. See [Webhook events](https://developer.webex.com/docs/task-routing-work-items#webhook-events) for an example.

**Important request fields inside `channelProperties`:**

| Field | Description | Mandatory |
| --- | --- | --- |
| `channelType` | Must be `workItem`, matching the existing task | Yes |
| `channel` | Channel specified in the Create Task request | Yes |
| `message.type` | Must be `work-item-form` | Yes |
| `message.direction` | Must be lowercase `inbound` | Yes |
| `message.aliasId` | Optional developer-provided message reference, up to 200 characters | No |
| `message.workItemData` | Nonempty string key/value object containing the fields to update | Yes |
| `message.timestampEpoch` | Message time as an integer in epoch milliseconds | Yes |

The schema and payload rules under [Work Item schema behavior](https://developer.webex.com/docs/task-routing-work-items#work-item-schema-behavior) also apply here. A channel or channel-type mismatch can be detected after HTTP acceptance and reported through `task-message:append-failed` with reason `INVALID_CONTENT`.

**Common failures**

Common Work Item update failure categories surfaced through `task-message:append-failed` include:

| Failure reason | Typical meaning | Typical next step |
| --- | --- | --- |
| `INVALID_CONTENT` | The update violates schema rules, contains an invalid required-field value, or does not match the task's channel/channel type. | Correct the payload to match the schema and the channel used in Create Task, then retry. |
| `NOT_FOUND` | The referenced task context could not be found. | Verify the task identifier before retrying. |
| `INTERNAL_ERROR` | The platform could not complete the update because of an unexpected internal failure. | Investigate the related failure event and retry. |

These reasons are representative. Some invalid requests are rejected in the HTTP response before acceptance and do not produce an asynchronous failure notification.

### Retry guidance

Assign a UUID to `channelProperties.message.aliasId` for each logical Work Item update and reuse that UUID if the same request needs to be retried. Use a different UUID for each new update. If you retry with the same UUID `aliasId`, the platform reuses that UUID as the API response `data.id` and the corresponding notification `id`. If `aliasId` is omitted, null, empty or not a UUID, the platform generates a new event ID for every request, including retries.

After `202 Accepted`, wait for the matching `task-message:appended` or `task-message:append-failed` notification before deciding whether to retry.
