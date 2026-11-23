---
type: Excerpt
canonical_url: https://developer.webex.com/docs/task-routing-work-items
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Update Work Item Data
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/task-routing-work-items). [Full Markdown](../../../../docs/task-routing-work-items.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before You Begin](003-before-you-begin.md)

## Article introduction

Work Items enable external systems to inject non-conversational tasks into Webex Contact Center and can be orchestrated within Webex CC Flow Designer, routed, handled, monitored, and reported alongside other contact center channel interactions.

**Note:** 
- Work Items do NOT represent live messaging conversations for unsupported channels such as Viber, Instagram, third-party digital channel gateways, etc. A bring-your-own messaging channel should be used for such use cases.
- Use Work Items specifically for backend or offline tasks such as CRM leads, claims, faxes, cases, purchase orders, or other work that needs contact center routing and agent handling without a customer messaging on the other side.

Availability for Work Items is currently open for **BETA**. Contact your Cisco team to request access.

## Selected section

## Update Work Item Data

Use the [Task Messages API](https://developer.webex.com/webex-contact-center/docs/api/v1/tasks-call-control/append-task-message) to append a subsequent snapshot of the Work Item data to the same task.

For Work Items, this API appends a metadata update. It does not append a conversational chat message.

**Example request:**
```json
{
	"channelParams": {
		"type": "work-item-form",
		"message": {
			"type": "WorkItemForm",
			"aliasId": "991d52ea-927f-41ff-832b-d8f8601a8fbd",
			"workItemData": {
				"customerAccountId": "3572653863",
				"customerAccountName": "Updated Customer Name",
				"claimStatus": "Approved"
			},
			"timestamp": 1779789108649
		}
	}
}
```

**Example response:**

```json

{
	"meta": {
		"orgId": "cb5901fb-ab66-4377-a7bc-5f0b21896952"
	},
	"data": {
		"id": "991d52ea-927f-41ff-832b-d8f8601a8fbd"
	}
}

```

- Use `data.id` as the update event correlation identifier. If request `aliasId` is a valid UUID, the platform can reuse that value as the event identifier.
- After a successful update, Webex Contact Center publishes the inbound `task-message:appended` subscription webhook for the same Work Item update, and the detailed event payload is documented in [Webhook Event Details](https://developer.webex.com/docs/webhooks-cc).

**Important request fields:**

- `channelParams.type`: Must be `work-item-form`
- `channelParams.message.aliasId`: Developer-provided Work Item update identifier for correlation
- `channelParams.message.workItemData`: Metadata fields to append to the Work Item transcript
- `channelParams.message.timestamp`: Work Item update timestamp in epoch milliseconds

**Common failures**

Common Work Item update failure categories surfaced through `task-message:append-failed` are shown below, and the detailed event payload is documented in [Webhook Event Details](https://developer.webex.com/docs/webhooks-cc):

| Failure reason    | Typical meaning                                                                                                               | Typical next step                                |
| ----------------- | ----------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------ |
| `INVALID_CONTENT` | The request payload violates Work Item schema or validation rules, such as missing required fields or invalid `workItemData`. | Correct the request payload and retry.           |
| `NOT_FOUND`       | The referenced task context could not be found.                                                                               | Verify the task identifier before retrying.      |
| `INTERNAL_ERROR`  | The platform could not complete the update because of an unexpected internal failure.                                         | Investigate the related failure event and retry. |
  
