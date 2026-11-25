---
type: Excerpt
canonical_url: https://developer.webex.com/docs/receive-and-verify-contact-center-webhooks
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Operate your receiver
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/receive-and-verify-contact-center-webhooks). [Full Markdown](../../../../docs/receive-and-verify-contact-center-webhooks.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md)

## Article introduction

Receive Webex Contact Center webhook events, verify their signatures, and acknowledge deliveries after durable acceptance.

## Selected section

## Operate your receiver

Track acceptance latency against the five-second response limit, registry/queue failures, signature and timestamp rejection counts, queue backlog, and worker processing failures. Keep payloads, tokens, secrets, and signatures out of application logs. Use event and subscription IDs for correlation.

A successful acknowledgement means the event was durably accepted. Record business processing completion separately, retry failed work idempotently, and reconcile resource state after missed deliveries or application outages. The API does not provide a universal replay operation for every resource.
