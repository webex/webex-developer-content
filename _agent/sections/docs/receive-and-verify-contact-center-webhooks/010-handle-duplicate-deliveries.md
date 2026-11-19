---
type: Excerpt
canonical_url: https://developer.webex.com/docs/receive-and-verify-contact-center-webhooks
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Handle duplicate deliveries
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/receive-and-verify-contact-center-webhooks). [Full Markdown](../../../../docs/receive-and-verify-contact-center-webhooks.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md)

## Article introduction

Receive Webex Contact Center webhook events, verify their signatures, and acknowledge deliveries after durable acceptance.

## Selected section

## Handle duplicate deliveries

The envelope's `id` identifies a source event and may be shared by multiple notifications for that event. Use `id` to deduplicate the event across subscriptions, or the `source` and `id` pair to deduplicate repeat deliveries within one subscription. Atomically persist your chosen key with the accepted event, or make your durable queue and worker enforce that scope. Keep downstream side effects idempotent. See [delivery considerations](https://developer.webex.com/docs/receive-and-verify-contact-center-webhooks#delivery-ordering-and-reconciliation) for reconciliation and ordering.

<a id="example-nodejs-app"></a>
