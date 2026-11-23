---
type: Excerpt
canonical_url: https://developer.webex.com/docs/using-webhooks
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Migrate from V1 to V2 Subscriptions
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/using-webhooks). [Full Markdown](../../../../docs/using-webhooks.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md)

## Article introduction

Create and manage Contact Center subscriptions, choose event resource versions, and migrate existing V1 subscriptions to V2.

## Selected section

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
