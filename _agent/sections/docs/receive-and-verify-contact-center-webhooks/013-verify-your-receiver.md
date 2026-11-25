---
type: Excerpt
canonical_url: https://developer.webex.com/docs/receive-and-verify-contact-center-webhooks
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Verify your receiver
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/receive-and-verify-contact-center-webhooks). [Full Markdown](../../../../docs/receive-and-verify-contact-center-webhooks.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md)

## Article introduction

Receive Webex Contact Center webhook events, verify their signatures, and acknowledge deliveries after durable acceptance.

## Selected section

## Verify your receiver

Configure a test subscription and secret in your registry. For V1 or V2, compute a fresh HMAC-SHA256 digest over the exact JSON body bytes using that secret and put its hex value in `X-WebexCC-Signature`; do not reuse the illustrative signature above. For V2, first replace both timestamp values with the same current Unix time in milliseconds, then compute the digest over that updated body. Confirm that a valid request is durably accepted before receiving `202`.

Then change the body without recomputing its signature, omit or corrupt the signature, and send mismatched or out-of-window V2 timestamps. Each must stop before enqueueing. Confirm that a registry or queue outage returns `503`, and that duplicate deliveries cannot repeat downstream side effects. Acknowledgement, signature verification, timestamp validation, and deduplication are separate checks.
