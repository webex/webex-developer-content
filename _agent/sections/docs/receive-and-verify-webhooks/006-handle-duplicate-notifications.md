---
type: Excerpt
canonical_url: https://developer.webex.com/docs/receive-and-verify-webhooks
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Handle duplicate notifications
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/receive-and-verify-webhooks). [Full Markdown](../../../../docs/receive-and-verify-webhooks.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md)

## Article introduction

Receive Webex Webhooks API notifications, verify signatures over the original request bytes, and process accepted events without repeating side effects.

## Selected section

## Handle duplicate notifications

Your app can receive more than one notification for an event. Make your webhook handler idempotent so processing the same notification again does not repeat a side effect, such as creating a second record or sending a second message. If the documentation for an event defines a stable event identifier, record it durably and check it before applying side effects. Otherwise, make updates safe to repeat and use the event and resource data to determine whether an action is still needed. Durable queues and idempotent processing are common ways to handle webhook delivery safely.

In the Webex webhook envelope, `id` identifies the webhook configuration; it is not a unique event or delivery identifier. Do not use that field by itself to deduplicate events, and do not assume a resource ID identifies a particular event.
