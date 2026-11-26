---
type: Excerpt
canonical_url: https://developer.webex.com/docs/task-routing-work-items
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Related APIs And Guides
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

## Related APIs And Guides

- [Authentication guide](https://developer.webex.com/docs/authentication)
- [Integrations guide](https://developer.webex.com/docs/integrations)
- [Create Task API](https://developer.webex.com/webex-contact-center/docs/api/v1/tasks-call-control/create-task)
- [Task Messages API](https://developer.webex.com/webex-contact-center/docs/api/v1/tasks-call-control/append-task-message)
- [End Task API](https://developer.webex.com/webex-contact-center/docs/api/v1/tasks-call-control/end-task)
- [Subscriptions API](https://developer.webex.com/webex-contact-center/docs/api/v2/subscriptions)
- [List Event Types API](https://developer.webex.com/webex-contact-center/docs/api/v2/subscriptions/list-event-types)
- [Webhooks guide](https://developer.webex.com/docs/webhooks-cc)
- [Using Webhooks](https://developer.webex.com/docs/using-webhooks)
- [Captures API](https://developer.webex.com/webex-contact-center/docs/api/v1/captures/list-captures)
