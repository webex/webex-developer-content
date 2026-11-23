---
type: Excerpt
canonical_url: https://developer.webex.com/docs/task-routing-work-items
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Create a new work item
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

## Create a new work item

Use the [Create Task API](https://developer.webex.com/webex-contact-center/docs/api/v1/tasks-call-control/create-task) to create the initial Work Item task.

**Example request:**

```json
{
	"origin": {
		"id": "<origin-identifier>",
		"name": "<customer-name>"
	},
	"destination": {
		"id": "<your-biz-address>",
		"type": "businessAddress"
	},
	"channelType": "workItem",
	"channel": "<work-item-custom-channel-name>",
	"flowSettings": {
		"foo": "bar"
	},
	"globalVariables": {
		"var1": "val1"
	},
	"channelParams": {
		"type": "work-item-form",
		"message": {
			"aliasId": "51b8f31d-05b2-45f8-b172-63920f2b7d9a",
			"workItemData": {
				"customerAccountId": "3572653863",
				"customerAccountName": "Customer Name",
				"claimNumber": "CLM1234567",
				"priority": "High"
			},
			"timestamp": 1779785508649
		}
	}
}
```

**Important request fields:**

| Parameter                            | Description                                                                            | Mandatory |
| ------------------------------------ | -------------------------------------------------------------------------------------- | --------- |
| `origin.id`                          | Developer-defined customer / case / task, or source-system identifier                  | Yes       |
| `origin.name`                        | Display name associated with the Work Item origin. Will appear as the ANI in reporting | No        |
| `destination.id`                     | Business address configured on the Work Item asset                                     | Yes       |
| `destination.type`                   | Must be `businessAddress`                                                              | Yes       |
| `channelType`                        | Must be `workItem`                                                                     | Yes       |
| `channel`                            | Configured `Work Item Channel Name`                                                    | Yes       |
| `flowSettings`                       | Flow variables supplied to the task                                                    | No        |
| `globalVariables`                    | Global variables mapped to the task                                                    | No        |
| `channelParams.type`                 | Must be `work-item-form`                                                               | Yes       |
| `channelParams.message.aliasId`      | Developer-provided Work Item data identifier for correlation. Set it to a UUID         | Yes       |
| `channelParams.message.workItemData` | Metadata fields that conform to the Work Item asset schema                             | Yes       |
| `channelParams.message.timestamp`    | Work Item timestamp in epoch milliseconds                                              | Yes       |

The guide shows one representative Work Item example. For the full set of supported request combinations and validation rules, refer to the [Create Task API](https://developer.webex.com/webex-contact-center/docs/api/v1/tasks-call-control/create-task).

**Example response:**

```json

{
	"meta": {
		"orgId": "cb5901fb-ab66-4377-a7bc-5f0b21896952"
	},
	"data": {
		"id": "141897a0-6212-49be-be9d-4823ab1e4dc7"
	}
}

```

Use `data.id` as the created task identifier. You should retain this value for subsequent Task Messages API calls and to correlate later task lifecycle subscription webhooks for the interaction.
