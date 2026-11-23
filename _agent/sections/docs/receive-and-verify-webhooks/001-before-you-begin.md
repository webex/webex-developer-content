---
type: Excerpt
canonical_url: https://developer.webex.com/docs/receive-and-verify-webhooks
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Before you begin
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/receive-and-verify-webhooks). [Full Markdown](../../../../docs/receive-and-verify-webhooks.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Receive Webex Webhooks API notifications, verify signatures over the original request bytes, and process accepted events without repeating side effects.

## Selected section

## Before you begin

[Register a webhook](https://developer.webex.com/docs/register-and-manage-webhooks) with a publicly reachable HTTPS destination and a unique secret. Store each registration's ID, secret, expected resource, event, and ownership information. This page covers the Webhooks API; Contact Center Subscriptions use [different envelope and signature rules](https://developer.webex.com/docs/receive-and-verify-contact-center-webhooks).
