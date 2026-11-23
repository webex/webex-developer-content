---
type: Excerpt
canonical_url: https://developer.webex.com/docs/task-routing-work-items
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Work Item schema behavior
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

## Work Item schema behavior

As mentioned previously, Work Item schema is configured on the Work Item asset. The schema controls the metadata fields that can be supplied when creating or updating a Work Item.

For Work Item API requests:
- `workItemData` must contain at least one field
- Field keys must match keys configured in the Work Item asset schema
- Required schema fields must be present and non-empty
- Required fields sent with `null` are treated as empty
- Values are validated against configured schema constraints
- Invalid, missing, unknown, or empty required fields can cause the request to fail

**Note:**  
- Work Items do NOT support attachments currently.
- They can only be supported in inbound direction.
