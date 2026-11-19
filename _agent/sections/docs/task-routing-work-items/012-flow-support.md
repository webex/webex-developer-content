---
type: Excerpt
canonical_url: https://developer.webex.com/docs/task-routing-work-items
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Flow Support
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

## Flow Support  

Work Item flows support self-service and routing activities that apply to non-conversational tasks.

Supported Work Item flow activities include:

- `Wait`
- `BRE Request`
- `Condition`
- `Go To`
- `HTTP Request`
- `Case`
- `Parse`
- `End Flow`
- `Percent Allocation`
- `Set Variable`
- `Business Hours`
- `Screen Pop`
- `Set Contact Priority`
- `Escalate CDG`
- `Get Queue Info`
- `Advanced Queue Info`
- `Queue Contact`
- `Queue To Agent`

**Note:** 

- Work Item start-node variables include interaction, entry point, organization, flow, origin, destination, and media payload details. The media payload includes the Work Item metadata supplied in `workItemData`.
- Call handling activities are not shown in Work Item flows. Custom Messaging Send and Receive nodes are not shown in Work Item flows.
