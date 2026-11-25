---
type: Excerpt
canonical_url: https://developer.webex.com/docs/receive-and-verify-contact-center-webhooks
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Identifying event version (2.0 based subscriptions only)
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/receive-and-verify-contact-center-webhooks). [Full Markdown](../../../../docs/receive-and-verify-contact-center-webhooks.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md)

## Article introduction

Receive Webex Contact Center webhook events, verify their signatures, and acknowledge deliveries after durable acceptance.

## Selected section

## Identifying event version (2.0 based subscriptions only)

With V2 based subscriptions, the event request contains the `X-WebexCC-Webhook-Version` header indicating the event resource version. Require that header to match the resource version you stored when registering the subscription before choosing a payload schema or accepting the event. Reject a missing or mismatched value; the HMAC covers the body, not this header.

You would want to migrate your subscription to newer version of events (as and when it's released), to get the best and latest of contact center webhook events. Older version of events will become inactive at some point in time.

<a id="response"></a>
