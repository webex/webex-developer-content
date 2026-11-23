---
type: Excerpt
canonical_url: https://developer.webex.com/docs/task-routing-work-items
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Webhook events
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

## Webhook events

Use the [Subscriptions API](https://developer.webex.com/webex-contact-center/docs/api/v1/subscriptions) for task lifecycle and Work Item update webhook events.

Important event families for Work Item integrations include:

- `task:new`
- `task:failed`
- `task-message:appended`
- `task-message:append-failed`

Use the [List Event Types API](https://developer.webex.com/webex-contact-center/docs/api/v1/subscriptions/list-event-types) to discover the latest supported event types and resource versions.

Use the [Webhooks guide](https://developer.webex.com/docs/webhooks-cc) for detailed task and task-message event payload documentation.

For Work Items, subscription-based `task-message:appended` and `task-message:append-failed` describe Work Item metadata updates. They do not represent customer chat messages.

**Representative work item `task-message:appended` subscription webhook**

```json
{
	"id": "4c2c4890-8a36-4dcc-9702-4c3a4aa1dc51",
	"specversion": "1.0",
	"type": "task-message:appended",
	"source": "/com/cisco/wxcc/ed9357d0-3f5d-4c6a-a4fd-111111111111",
	"comciscoorgid": "cb5901fb-ab66-4377-a7bc-5f0b21896952",
	"comciscotimestamp": 1779789108649,
	"datacontenttype": "application/json",
	"data": {
		"taskId": "141897a0-6212-49be-be9d-4823ab1e4dc7",
		"direction": "INBOUND",
		"messageDirection": "INBOUND",
		"channelType": "workItem",
		"channel": "ClaimsReview",
		"origin": "crm-lead-10040",
		"destination": "claims-work-items@example.biz",
		"createdTime": 1779789108649,
		"eventDetails": "Appended Work Item data successfully.",
		"channelParams": {
			"type": "work-item-form",
			"message": {
				"aliasId": "991d52ea-927f-41ff-832b-d8f8601a8fbd",
				"workItemData": {
					"customerAccountId": "3572653863",
					"customerAccountName": "Updated Customer Name",
					"claimStatus": "Approved"
				},
				"timestamp": 1779789108649,
				"type": "WorkItemForm"
			}
		},
		"reason": null,
		"errorMessage": null
	}
}
```

**Representative `task:failed` subscription webhook**

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
		"taskId": "141897a0-6212-49be-be9d-4823ab1e4dc7",
		"origin": "crm-lead-10040",
		"destination": "claims-work-items@example.biz",
		"direction": "INBOUND",
		"channel": "ClaimsReview",
		"channelType": "workItem",
		"mediaMgr": "digitalmm",
		"reason": "ENTRY_POINT_NOT_FOUND",
		"errorMessage": "The Work Item asset does not resolve to an active entry point.",
		"failureType": "failed",
		"createdTime": 1779785508649
	}
}

```
**Common failures**
  
  Common cases that can result in `task:failed` include:

- `CHANNEL_ASSET_UNDEFINED`: the destination business address does not resolve to a valid Work Item asset
- `FEATURE_FLAG_DISABLED`: the organization is not enabled for Work Items
- `ENTRY_POINT_NOT_FOUND`: the asset does not resolve to an active entry point
- `ORG_DIGITAL_CONTACT_LIMIT_EXCEEDED`: the organization has reached its active digital contact limit
- `CONVERSATION_CREATION_FAILED`: downstream Work Item creation failed after the request was accepted
- Validation failures, such as missing required schema fields or invalid `workItemData`

**Representative `task-message:append-failed` subscription webhook:**

```json

{
	"id": "64ab4f4a-5c93-4339-b325-3878f289a88f",
	"specversion": "1.0",
	"type": "task-message:append-failed",
	"source": "/com/cisco/wxcc/ed9357d0-3f5d-4c6a-a4fd-333333333333",
	"comciscoorgid": "cb5901fb-ab66-4377-a7bc-5f0b21896952",
	"comciscotimestamp": 1779789108649,
	"datacontenttype": "application/json",
	"data": {
		"taskId": "141897a0-6212-49be-be9d-4823ab1e4dc7",
		"direction": "INBOUND",
		"messageDirection": "INBOUND",
		"channelType": "workItem",
		"channel": "ClaimsReview",
		"origin": "crm-lead-10040",
		"destination": "claims-work-items@example.biz",
		"createdTime": 1779789108649,
		"eventDetails": null,
		"channelParams": null,
		"reason": "INVALID_CONTENT",
		"errorMessage": "Required Work Item schema field claimNumber is missing."
	}
}
```
Use the following fields to correlate Work Item webhook processing

- `data.taskId`: task identifier
- `data.channelParams.message.aliasId`: Developer defined Work Item identifier for `task-message:appended` when `channelParams` is present
- `data.channelParams.message.workItemData`: Work Item metadata for the create or update
- `id`: webhook event identifier
