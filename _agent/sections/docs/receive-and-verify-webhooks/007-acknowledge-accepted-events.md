---
type: Excerpt
canonical_url: https://developer.webex.com/docs/receive-and-verify-webhooks
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Acknowledge accepted events
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/receive-and-verify-webhooks). [Full Markdown](../../../../docs/receive-and-verify-webhooks.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md)

## Article introduction

Receive Webex Webhooks API notifications, verify signatures over the original request bytes, and process accepted events without repeating side effects.

## Selected section

## Acknowledge accepted events

Verify the signature and validate the delivery against your stored registration before processing it. Return a successful 2xx response only after processing has completed or durable storage has accepted the event for a worker. Acknowledge durable acceptance separately from completion of the business action. Make worker retries safe to repeat.

Treat payloads as sensitive. Log correlation IDs and outcomes rather than tokens, signing secrets, signatures, or message contents. Track delivery acceptance failures, verification failures, queue backlog, and processing failures in your application.
