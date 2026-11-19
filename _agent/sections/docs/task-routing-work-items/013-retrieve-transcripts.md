---
type: Excerpt
canonical_url: https://developer.webex.com/docs/task-routing-work-items
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Retrieve Transcripts
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

## Retrieve Transcripts

Use the [Captures API](https://developer.webex.com/webex-contact-center/docs/api/v1/captures/list-captures) to retrieve post-interaction transcripts for Work Item tasks.

Work Item transcripts contain metadata snapshots rather than conversational messages.

**Representative Work Item transcript entries:**

```json

[
	{
		"id": "51b8f31d-05b2-45f8-b172-63920f2b7d9a",
		"aliasId": "51b8f31d-05b2-45f8-b172-63920f2b7d9a",
		"direction": "inbound",
		"workItemData": {
			"customerAccountId": "3572653863",
			"customerAccountName": "Customer Name",
			"claimNumber": "CLM1234567",
			"priority": "High"
		},
		"timestamp": "2026-06-04T10:24:22.909Z"
	},
	{
		"id": "991d52ea-927f-41ff-832b-d8f8601a8fbd",
		"aliasId": "991d52ea-927f-41ff-832b-d8f8601a8fbd",
		"direction": "inbound",
		"workItemData": {
			"claimStatus": "Approved"
		},
		"timestamp": "2026-06-04T10:28:11.000Z"
	}
]
```
Work Item transcripts are retrieved after transcript generation, subject to retention and capture availability.

  
