---
type: Excerpt
canonical_url: https://developer.webex.com/docs/receive-and-verify-contact-center-webhooks
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Receiving Webhooks
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/receive-and-verify-contact-center-webhooks). [Full Markdown](../../../../docs/receive-and-verify-contact-center-webhooks.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md)

## Article introduction

Receive Webex Contact Center webhook events, verify their signatures, and acknowledge deliveries after durable acceptance.

## Selected section

## Receiving Webhooks

We draw inspiration from the CloudEvents.io [JSON format](https://github.com/cloudevents/spec/blob/v1.0.1/json-format.md#32-examples), [HTTP Structured Content Mode](https://github.com/cloudevents/spec/blob/v1.0.1/http-protocol-binding.md#32-structured-content-mode), and [Webhook](https://github.com/cloudevents/spec/blob/v1.0.1/http-webhook.md) specifications. The main areas in which we differ are Webhook authorization, and managing request rates and 429s.

If you are not familiar with CloudEvents spec, do not worry. Here's what you need to know:

<a id="anatomy-of-a-webhook"></a>
