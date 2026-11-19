---
type: Excerpt
canonical_url: https://developer.webex.com/docs/receive-and-verify-contact-center-webhooks
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Request Verification
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/receive-and-verify-contact-center-webhooks). [Full Markdown](../../../../docs/receive-and-verify-contact-center-webhooks.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md)

## Article introduction

Receive Webex Contact Center webhook events, verify their signatures, and acknowledge deliveries after durable acceptance.

## Selected section

## Request Verification

To verify requests are originating from Webex Contact Center, are authentic, and are unmodified, you may verify webhooks using a cryptographic signature. Receivers are strongly encouraged to implement this feature for their own security.

When a Subscription is registered, a `secret` may be provided. Providing a `secret` causes our system to include the `X-WebexCC-Signature` header in webhooks. To verify a webhook, you must supply the unmodified request body and Subscription's secret to the HMAC-SHA256 algorithm, then compare the hex-encoded output with the header's value in constant time. Reject a missing, malformed, or invalid signature before processing the event. If they match, then the webhook is valid. Note that this system relies on the provided `secret` field being confidential.

Built-ins or packages exist for most language ecosystems for taking HMAC signatures. The sample code, below, implements this check in Node.

<a id="replay-attack-prevention-20-based-subscriptions-only"></a>
