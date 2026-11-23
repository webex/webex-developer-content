---
type: Excerpt
canonical_url: https://developer.webex.com/docs/receive-and-verify-webhooks
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Troubleshoot delivery
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/receive-and-verify-webhooks). [Full Markdown](../../../../docs/receive-and-verify-webhooks.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md)

## Article introduction

Receive Webex Webhooks API notifications, verify signatures over the original request bytes, and process accepted events without repeating side effects.

## Selected section

## Troubleshoot delivery

| Symptom | Check |
| --- | --- |
| No delivery after registration | Confirm the registration is active, the expected event occurred, filters match an accessible resource, and Webex can reach the HTTPS endpoint. For Calling, inspect applicable interest registrations and expiration. |
| Signature mismatch | Use the secret for this registration and the unmodified body bytes. Look up header names case-insensitively. Parse the newer header's algorithm/digest pairs instead of comparing a digest to the whole header. |
| Message text is absent | Fetch the resource with your application token; see [Handling Sensitive Data](https://developer.webex.com/docs/receive-and-verify-webhooks#handling-sensitive-data). |
| A Meeting REST lookup returns 404 after an event | See [Data Synchronization Meetings](https://developer.webex.com/docs/receive-and-verify-webhooks#data-synchronization-meetings) before treating the resource as absent. |
| Duplicate actions | Inspect the idempotency strategy and durable worker state. Do not deduplicate all events using the registration ID. |
| Deliveries stopped after endpoint failures | Inspect status and follow [Disabled Webhooks](https://developer.webex.com/docs/receive-and-verify-webhooks#disabled-webhooks). Correct the endpoint failure before reenabling delivery. |
