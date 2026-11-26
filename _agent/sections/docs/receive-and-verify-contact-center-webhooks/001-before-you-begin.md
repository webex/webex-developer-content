---
type: Excerpt
canonical_url: https://developer.webex.com/docs/receive-and-verify-contact-center-webhooks
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Before you begin
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/receive-and-verify-contact-center-webhooks). [Full Markdown](../../../../docs/receive-and-verify-contact-center-webhooks.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Receive Webex Contact Center webhook events, verify their signatures, and acknowledge deliveries after durable acceptance.

## Selected section

## Before you begin

[Create and manage a subscription](https://developer.webex.com/docs/using-webhooks#customer-onboarding-page) with a unique secret and a publicly reachable HTTPS receiver. Your application must store each subscription's ID, customer organization, secret, API version, and configured resource version. See [Register and manage subscriptions](https://developer.webex.com/docs/using-webhooks) for registration and V1-to-V2 migration, and [Event reference](https://developer.webex.com/docs/webhooks-cc) for resource versions and event-specific data.

This page covers Contact Center Subscriptions webhooks. For Messaging, Meetings, Calling, and administration events registered with the Webhooks API, use the [Webex Webhooks API receiver guide](https://developer.webex.com/docs/receive-and-verify-webhooks); its signature headers and envelope are different.
