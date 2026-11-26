---
type: Excerpt
canonical_url: https://developer.webex.com/docs/task-routing-work-items
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Retrieve Transcripts
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

## Retrieve Transcripts

Use the [Captures API](https://developer.webex.com/webex-contact-center/docs/api/v1/captures/list-captures) to retrieve post-interaction transcripts for Work Item tasks.

Work Item transcripts contain metadata snapshots rather than conversational messages. Unlike the notification's message metadata, transcript entries can include `workItemData`.

**Representative Work Item transcript entries:**

The following excerpt shows the identifiers, timestamps and Work Item data for the creation and update examples. Other transcript fields are omitted for clarity.

```json
[
  {
    "id": "22222222-2222-4222-8222-222222222222",
    "aliasId": "51b8f31d-05b2-45f8-b172-63920f2b7d9a",
    "direction": "inbound",
    "workItemData": {
      "customerAccountId": "account-001",
      "customerAccountName": "Customer Name",
      "claimNumber": "CLM-001",
      "priority": "High",
      "claimStatus": "New"
    },
    "timestamp": "2026-05-26T08:51:48.649Z"
  },
  {
    "id": "44444444-4444-4444-8444-444444444444",
    "aliasId": "991d52ea-927f-41ff-832b-d8f8601a8fbd",
    "direction": "inbound",
    "workItemData": {
      "claimStatus": "Approved"
    },
    "timestamp": "2026-05-26T09:51:48.649Z"
  }
]
```

Transcript entry `id` identifies the stored message. Its `aliasId` is the supplied or generated message alias; neither should be assumed to equal the notification event ID.

Work Item transcripts are retrieved after transcript generation, subject to retention and capture availability.
