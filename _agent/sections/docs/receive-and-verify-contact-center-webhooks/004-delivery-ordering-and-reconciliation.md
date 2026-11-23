---
type: Excerpt
canonical_url: https://developer.webex.com/docs/receive-and-verify-contact-center-webhooks
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Delivery, ordering, and reconciliation
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/receive-and-verify-contact-center-webhooks). [Full Markdown](../../../../docs/receive-and-verify-contact-center-webhooks.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md)

## Article introduction

Receive Webex Contact Center webhook events, verify their signatures, and acknowledge deliveries after durable acceptance.

## Selected section

## Delivery, ordering, and reconciliation

Contact Center integrations should reconcile webhook-driven state with the relevant resource APIs. Delivery can be missed. Choose a reconciliation schedule and query windows appropriate to the resource and your application; consult resource-specific recovery APIs in the [event reference](https://developer.webex.com/docs/webhooks-cc).

Contact Center events can arrive out of order. Check resource state and event timestamps before applying stateful updates. Do not assume arrival order represents resource state order.

See [Handle duplicate deliveries](https://developer.webex.com/docs/receive-and-verify-contact-center-webhooks#handle-duplicate-deliveries) for source-event identifiers and the durable acceptance boundary.

<a id="not-receiving-events"></a>
