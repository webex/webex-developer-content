---
type: Excerpt
canonical_url: https://developer.webex.com/docs/task-routing-work-items
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Responsibilities
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

## Responsibilities

### External developer

Your **middleware** will be mainly responsible for creating or updating Work Item tasks in Webex Contact Center. Below are the requirements that the developer is expected to manage:

- Hosting the middleware that receives or produces the external work item
- Obtaining and refreshing OAuth tokens to integrate with Webex CC's Task API
- Integration with Webex CC APIs as required - Tasks, Subscription, Search, Captures
- Ensuring that the `Work Item Data` conforms to the administrator-configured Work Item schema on the Asset configured on Control Hub
### Webex Contact Center

Webex Contact Center is responsible for:

- Validating Work Item task requests against configured assets, entry points, and schema
- Running the configured Work Item flow as configured against the Entry point
- Routing Work Items to queues and agents as per the configuration on Webex CC Flow Designer
- Presenting Work Item metadata to agents on the Desktop as read-only data
- Generating task lifecycle and Work Item update webhook events
- Exposing post interaction transcripts for Work Item containing snapshots of the data held within Webex CC.
