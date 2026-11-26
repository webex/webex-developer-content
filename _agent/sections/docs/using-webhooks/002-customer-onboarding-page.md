---
type: Excerpt
canonical_url: https://developer.webex.com/docs/using-webhooks
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Customer Onboarding Page
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/using-webhooks). [Full Markdown](../../../../docs/using-webhooks.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md)

## Article introduction

Create and manage Contact Center subscriptions, choose event resource versions, and migrate existing V1 subscriptions to V2.

## Selected section

## Customer Onboarding Page

Before your app can receive any webhooks, a user with an administrator role must opt in to send events to your service by creating a webhook Subscription. **Your app is responsible for building this onboarding page**.

A [Subscription](https://developer.webex.com/docs/api/v1/subscriptions) is how your app states which events it should be notified of, and where the notifications should be sent. When notifying your app of an event, we send POST requests to the `destinationUrl` field of the registered Subscription. This field has some restrictions; check the [Subscription API docs](https://developer.webex.com/docs/api/v1/subscriptions/register-subscription) for restrictions on this field. Use HTTPS on port 443 with a domain name and a path (at least `/`). Query parameters, URL credentials, fragments, and non-443 ports are not accepted. Keep tokens and API keys out of the destination URL.

### Authentication and Authorization

Consult our [Authentication guide](https://developer.webex.com/docs/authentication) on how to build a UI app with Cisco Common Identity. This is necessary because a Cisco Common Identity token is required to call the [Subscription APIs](https://developer.webex.com/docs/api/v1/subscriptions).

For user-token management calls, use an administrator authorized for the target organization, including an authorized partner/delegated administrator acting on its behalf. Create, update, and delete operations require `cjp:config_write`; list and get operations require `cjp:config_read`.

### Subscription Lifecycle and Onboarding Page Functionality

A Subscription resource is first registered, and may be updated, and then deleted. All of these functions must be supported by your page. If your Subscriptions were disabled (by the system or by API) or deleted, reenabling or recreating the Subscriptions would require a token.

An organization has an upper limit on the total number of Subscriptions. Ensure that you clean up Subscriptions and keep your total count low.

Use a unique secret of 32–256 characters. Keep the subscription ID and signing secret in your application registry when creating or updating a subscription. Subscription responses omit the secret, so a later list or get cannot recover it.

When you clean up Subscriptions, ensure that you remove your app's Subscriptions only. Use the `name`, `description`, or `destinationUrl` fields to find out which Subscriptions are managed by your app.
