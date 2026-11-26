---
type: Excerpt
canonical_url: https://developer.webex.com/docs/task-routing-work-items
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- How does this work?
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

## How does this work?

- Developers are expected to host an external system (a middleware) that owns the source task and work item metadata. This is expected to be developed by the partner or customer that integrates with upstream systems and injects tasks into Webex Contact Center.
- Webex Contact Center owns routing, flows, agent handling, task state, lifecycle events, and reporting
- Administrators configure the following entities on **Control Hub** at a high level:
  - **Work Item Channel:** Represents the custom channel that you plan to integrate with (e.g. Fax)
  - **Work Item Asset:** Represents an instance of the channel added above and establishes the data schema payloads you wish to honor when injecting tasks into Webex Contact Center
  - **Flow:** Represents the flow that manages orchestrating a work item and routing it to queues
  - **Queue:** Queues support the `Work Item` channel type
  - **Multimedia Profile:** Determines the no. of tasks an agent can work on in parallel either via automatic contact distribution or self-assignment (cherry picking)
- Developers use **Public APIs** for the following:
  - **Webhook events:** Subscribe to task lifecycle and message events using **Subscriptions API**
  - **Create work item:** Create a work item using **Create Task API v2**
  - **Update work item:** Update a work item's data using **Task Messages API**
  - **Search for work items:** To look up existing work items using **Search API**
  - **Retrieve transcripts:** Pull post interaction transcripts using **Captures API**
