---
type: Excerpt
canonical_url: https://developer.webex.com/docs/receive-and-verify-contact-center-webhooks
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Replay attack prevention (2.0 based subscriptions only)
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/receive-and-verify-contact-center-webhooks). [Full Markdown](../../../../docs/receive-and-verify-contact-center-webhooks.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md)

## Article introduction

Receive Webex Contact Center webhook events, verify their signatures, and acknowledge deliveries after durable acceptance.

## Selected section

## Replay attack prevention (2.0 based subscriptions only)

For V2 based subscriptions, we provide a timestamp indicating when the event was dispatched, as a part of body `comciscotimestamp` and header `X-WebExCC-Timestamp`. This timestamp, in conjunction with HMAC signatures, gives a way to validate when the event was sent out, and mitigate replay attacks.

After verifying the HMAC over the raw request bytes, require the timestamp header to match the signed timestamp in the body. Reject missing, malformed, mismatched, expired, or excessively future-dated timestamps. Choose a clock tolerance appropriate to your application; the example below uses five minutes in either direction. Determine whether V2 checks are required from your stored subscription configuration, rather than the presence of an incoming header. Keep receiver clocks synchronized. Timestamp validation limits replay age; it does not replace durable event deduplication within that window.

The sample code below contains a way to check this.

<a id="identifying-event-version-20-based-subscriptions-only"></a>
