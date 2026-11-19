---
type: Guide
title: Contact Center Webhooks | Register and manage subscriptions
display_title: Register and manage subscriptions
canonical_url: https://developer.webex.com/docs/using-webhooks
content_type: documentation
product_group:
- webex-contact-center
categories:
- create
- webex-contact-center
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/using-webhooks)

Create and manage Contact Center subscriptions, choose event resource versions, and migrate existing V1 subscriptions to V2.

## Before you begin

This page covers Contact Center Subscriptions. Choose an event and resource version from the [Contact Center event reference](https://developer.webex.com/docs/webhooks-cc), then configure a [receiver](https://developer.webex.com/docs/receive-and-verify-contact-center-webhooks). For platform Service App authorization events, use the [Webhooks API registration guide](https://developer.webex.com/docs/register-and-manage-webhooks).

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

## Migrate from V1 to V2 Subscriptions
In order to add versioning support for webhook events, V2 based Subscription APIs have been introduced.
You will be able to specify the version of webhook event you are interested in as part of the Subscription API.

Webhook events are versioned by resource. Select event types from one resource and a compatible resource version for each subscription.
Refer to the List Event Types `/v2/list-event-types` API for details on the latest available resources and versions.
V2 creation requires `resourceVersion` in `resource:version` form, such as `agent:1.0.0`. Select a currently supported version from List Event Types; do not assume every event is available in every version.

Use V2 for explicit event version selection. Check the current Subscription API reference and [developer support](https://developer.webex.com/support) for V1 support and retirement dates before planning a migration.

Manage V2 subscriptions through the `/v2` Subscription API and V1 subscriptions through `/v1`. Each version’s list returns its own subscriptions in `data`, while `meta.subscriptionCount` counts both versions in the organization. An empty `data` array does not establish that the organization has no subscriptions.

### Migration Guide

The following guide outlines the process for migrating from V1 based subscriptions to V2 based subscriptions.

1. Initiate Migration:

   Create a new subscription by utilizing the /v2 API. Ensure that the information provided aligns with your previous subscriptions established through the /v1 API.
   As part of the request, add a new field, `resourceVersion`, in the request body, with a value formatted as `resource:version`. For example, for agent resource, put `agent:1.0.0`
   Set a unique signing secret and configure raw-body signature verification. For V2, also validate the signed timestamp and stored resource version as described in the [receiver guide](https://developer.webex.com/docs/receive-and-verify-contact-center-webhooks).

2. Validate Integration with new subscription:

   Webhook events will be sent to both V1 and V2 based subscriptions as long as they exist. Validate your integration is working with the new subscription and you are able to receive webhook events.

3. Post validation:

   Once, verification is completed, delete the older subscription that is no longer needed using `/v1` Delete API.

## Receive your first event

1. Use [List Event Types](https://developer.webex.com/docs/api/v1/subscriptions/list-event-types) to choose a supported agent login event and its resource version.
2. Register a test subscription using the versioned Subscription API, your receiver's HTTPS `destinationUrl`, a unique signing secret, and the selected event/resource version. Follow the [Register Subscription reference](https://developer.webex.com/docs/api/v1/subscriptions/register-subscription) for its request fields; select the API version you intend to use.
3. Store the returned subscription ID, customer organization, signing secret, API version, and configured resource version in your application registry.
4. Trigger an agent login in the subscribed test organization. Expect an event with `type: agent:login`; validate its version and payload against the [event reference](https://developer.webex.com/docs/webhooks-cc#agent-login).
5. Confirm the receiver authenticates the delivery and accepts it durably before returning a 2xx response. Use the [receiver verification checklist](https://developer.webex.com/docs/receive-and-verify-contact-center-webhooks#verify-your-receiver).
6. Remove only your application's test subscription through the same API version used to create it. Remove its receiver registry entry and signing secret after cleanup.

## Delivery and recovery

See [delivery, ordering, and reconciliation](https://developer.webex.com/docs/receive-and-verify-contact-center-webhooks#delivery-ordering-and-reconciliation). Registration and authenticated management calls are separate from acknowledging incoming deliveries.

## Earlier receiver bookmarks

<a id="overview"></a>
<a id="use-cases"></a>

For an overview and product use cases, see [Webhooks overview](https://developer.webex.com/docs/webhooks#choose-a-webhook-family).

<a id="design-considerations"></a>

See [delivery, ordering, and reconciliation](https://developer.webex.com/docs/receive-and-verify-contact-center-webhooks#delivery-ordering-and-reconciliation).

<a id="receiving-webhooks"></a>

See [Receiving Webhooks](https://developer.webex.com/docs/receive-and-verify-contact-center-webhooks#receiving-webhooks).

<a id="anatomy-of-a-webhook"></a>

[Anatomy of a webhook](https://developer.webex.com/docs/receive-and-verify-contact-center-webhooks#anatomy-of-a-webhook).

<a id="not-receiving-events"></a>

[Not receiving events](https://developer.webex.com/docs/receive-and-verify-contact-center-webhooks#not-receiving-events).

<a id="request-verification"></a>

[Request verification](https://developer.webex.com/docs/receive-and-verify-contact-center-webhooks#request-verification).

<a id="replay-attack-prevention-20-based-subscriptions-only"></a>

[Replay attack prevention 20 based subscriptions only](https://developer.webex.com/docs/receive-and-verify-contact-center-webhooks#replay-attack-prevention-20-based-subscriptions-only).

<a id="identifying-event-version-20-based-subscriptions-only"></a>

[Identifying event version 20 based subscriptions only](https://developer.webex.com/docs/receive-and-verify-contact-center-webhooks#identifying-event-version-20-based-subscriptions-only).

<a id="response"></a>

[Response](https://developer.webex.com/docs/receive-and-verify-contact-center-webhooks#response).

<a id="code"></a>

[Code](https://developer.webex.com/docs/receive-and-verify-contact-center-webhooks#code).

<a id="latency"></a>

[Latency](https://developer.webex.com/docs/receive-and-verify-contact-center-webhooks#latency).

## Example Node.js app

Use the [receiver implementation and required registry/queue adapters](https://developer.webex.com/docs/receive-and-verify-contact-center-webhooks#example-nodejs-app).
