---
type: Excerpt
canonical_url: https://developer.webex.com/docs/using-webhooks
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Receive your first event
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/using-webhooks). [Full Markdown](../../../../docs/using-webhooks.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md)

## Article introduction

Create and manage Contact Center subscriptions, choose event resource versions, and migrate existing V1 subscriptions to V2.

## Selected section

## Receive your first event

1. Use [List Event Types](https://developer.webex.com/docs/api/v1/subscriptions/list-event-types) to choose a supported agent login event and its resource version.
2. Register a test subscription using the versioned Subscription API, your receiver's HTTPS `destinationUrl`, a unique signing secret, and the selected event/resource version. Follow the [Register Subscription reference](https://developer.webex.com/docs/api/v1/subscriptions/register-subscription) for its request fields; select the API version you intend to use.
3. Store the returned subscription ID, customer organization, signing secret, API version, and configured resource version in your application registry.
4. Trigger an agent login in the subscribed test organization. Expect an event with `type: agent:login`; validate its version and payload against the [event reference](https://developer.webex.com/docs/webhooks-cc#agent-login).
5. Confirm the receiver authenticates the delivery and accepts it durably before returning a 2xx response. Use the [receiver verification checklist](https://developer.webex.com/docs/receive-and-verify-contact-center-webhooks#verify-your-receiver).
6. Remove only your application's test subscription through the same API version used to create it. Remove its receiver registry entry and signing secret after cleanup.
