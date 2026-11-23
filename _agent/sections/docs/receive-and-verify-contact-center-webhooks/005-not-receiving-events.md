---
type: Excerpt
canonical_url: https://developer.webex.com/docs/receive-and-verify-contact-center-webhooks
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Not Receiving Events?
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/receive-and-verify-contact-center-webhooks). [Full Markdown](../../../../docs/receive-and-verify-contact-center-webhooks.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md)

## Article introduction

Receive Webex Contact Center webhook events, verify their signatures, and acknowledge deliveries after durable acceptance.

## Selected section

## Not Receiving Events?

Double-check:

- Events in Webex Contact Center are occurring.
- The subscription exists, is enabled, and has the correct `destinationUrl`.
- Your company/datacenter firewall could be blocking incoming HTTPS requests. Please note that we cannot provide IT with static IPs, as our cloud infrastructure is dynamic in nature.

<a id="request-verification"></a>
