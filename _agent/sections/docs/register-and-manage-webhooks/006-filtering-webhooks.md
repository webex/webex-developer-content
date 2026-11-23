---
type: Excerpt
canonical_url: https://developer.webex.com/docs/register-and-manage-webhooks
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Filtering Webhooks
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/register-and-manage-webhooks). [Full Markdown](../../../../docs/register-and-manage-webhooks.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md) [User Level Scopes for Meeting Related Webhooks](004-user-level-scopes-for-meeting-related-webhooks.md) [Organization/Admin/Compliance Officer Level Scopes for Meeting Related Webhooks](005-organization-admin-compliance-officer-level-scopes-for-meeti.md)

## Article introduction

Register Webex Webhooks API notifications for Messaging, Meetings, Calling, and platform events, then manage registrations owned by your application.

## Selected section

## Filtering Webhooks

In order to narrow down the data that you receive from webhooks, you can add filters to your webhooks. To do this, you can create a webhook for a resource that applies to an event, and then add a filter or a combination of filters to send you only notification content that is based on the added filter restrictions. For example, you can register a webhook for a membership resource and then add filters so that the webhook only applies to a specific room, by using its `roomId` filter.

You can also use more than one filter in a webhook. To use multiple filters, combine them with the “&” symbol. For example, to create a webhook that only sends notifications when a specific person performs an action in a specific room, such as sending a message or creating a membership, combine the `personEmail` and `roomId` filters: <code>personEmail=person@example.com&roomId=abc123</code>.



> **Info**
>
> When creating a meeting webhook with a filter of `hostEmail` or `hostUserId`, or a converged recordings webhook with a filter of `ownerEmail` or `ownerId`, `ownedBy` must be set to `org`.



See the [event reference](https://developer.webex.com/docs/webhook-event-reference) for the filters supported by each resource.



> **Warning**
>
> You can only use ID filters for resources you have access to. If you do not have access to a particular resource or ID filter, you will receive an error (such as `invalid value for filter: roomId`) from the API.



Alternatively, Webhooks also support what is commonly known as a “firehose” or “wildcard” webhook, which allows your app to subscribe to several commonly-used resources and/or events with a single webhook. For more information, see [The Firehose Webhook](https://developer.webex.com/docs/register-and-manage-webhooks#the-firehose-webhook).
