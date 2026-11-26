---
type: Excerpt
canonical_url: https://developer.webex.com/docs/task-routing-work-items
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Before You Begin
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/task-routing-work-items). [Full Markdown](../../../../docs/task-routing-work-items.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Work Items enable external systems to inject **non-conversational tasks** into Webex Contact Center and can be orchestrated within Webex CC Flow Designer, routed, handled, monitored, and reported alongside other contact center channel interactions.

---

New

**Note:** 
- Work Items do NOT represent live messaging conversations for unsupported channels such as Viber, Instagram, third-party digital channel gateways, etc. A bring-your-own messaging channel should be used for such use cases.
- Use Work Items specifically for backend or offline tasks such as CRM leads, claims, faxes, cases, purchase orders, or other work that needs contact center routing and agent handling without a customer messaging on the other side.

## Selected section

## Before You Begin

Before integrating, ensure that the administrator has configured the following in Control Hub:

- A `Work Item Custom Channel` with:
  - `Custom channel name`
  - `Logo` (optional)
- A `Work Item Asset` with:
  - `Asset name` and `Description` (optional)
  - `Business address` - Work Item assets use a configured business address to resolve Create Task requests. The business address must be unique across Work Item assets.
  - `Data schema fields` - The schema defines the Work Item metadata fields. Configure at least one required field and one viewable field before saving the asset. API payload limits and the rules for creating and updating these fields are described under [Work Item schema behavior](https://developer.webex.com/docs/task-routing-work-items#work-item-schema-behavior). A schema field includes:
    - `Field key`
    - `Display name`
    - Whether the field is `required`
    - Whether the field is `viewable`
    **Note:** At least 1 viewable and 1 required field is **mandatory**
- A `Work Item Entry Point` mapped to a `Work Item Asset` and a `Work Item Flow`
- `Work Item Queues` and queue ranking within relevant `Teams` as needed
- `Multimedia profile` capacity for Work Items. Please note that we support both **automatic-assignment** and **self-assignment** (cherry picking) similar to other digital channels.
- `RONA timeout` values for Work Items as needed
- Other Contact Center routing objects required for the interaction, such as teams, skills, queues, and agent profiles
