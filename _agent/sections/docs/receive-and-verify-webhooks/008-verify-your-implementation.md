---
type: Excerpt
canonical_url: https://developer.webex.com/docs/receive-and-verify-webhooks
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Verify your implementation
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/receive-and-verify-webhooks). [Full Markdown](../../../../docs/receive-and-verify-webhooks.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md)

## Article introduction

Receive Webex Webhooks API notifications, verify signatures over the original request bytes, and process accepted events without repeating side effects.

## Selected section

## Verify your implementation

Use the synthetic body and secret in [Authenticating Requests](https://developer.webex.com/docs/receive-and-verify-webhooks#authenticating-requests) only as a local test fixture. Compute the HMAC over the exact bytes, including the absence of a trailing newline, and compare against the documented SHA-256 and SHA-512 values.

Check a valid delivery, then modify its body without updating the signature, remove the signature, provide a malformed digest, and provide an unsupported algorithm label. Invalid requests must stop before a business action or enqueue operation. Test both supported signature contracts that your webhook type actually emits; do not assume every resource sends `X-Webex-Signature`.

Deliver the same event twice and confirm it cannot repeat a side effect. The registration `id` is not a unique event identifier. Confirm that a failed durable acceptance cannot produce a successful acknowledgement.
