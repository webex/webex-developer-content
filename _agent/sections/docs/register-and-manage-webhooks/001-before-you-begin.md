---
type: Excerpt
canonical_url: https://developer.webex.com/docs/register-and-manage-webhooks
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Before you begin
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/register-and-manage-webhooks). [Full Markdown](../../../../docs/register-and-manage-webhooks.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [User Level Scopes for Meeting Related Webhooks](004-user-level-scopes-for-meeting-related-webhooks.md) [Organization/Admin/Compliance Officer Level Scopes for Meeting Related Webhooks](005-organization-admin-compliance-officer-level-scopes-for-meeti.md)

## Article introduction

Register Webex Webhooks API notifications for Messaging, Meetings, Calling, and platform events, then manage registrations owned by your application.

## Selected section

## Before you begin

This page covers `/v1/webhooks`. Contact Center event subscriptions use a [different registration guide](https://developer.webex.com/docs/using-webhooks). A Contact Center application still uses this guide when subscribing to platform Service App authorization events.

Choose a resource and event from the [event reference](https://developer.webex.com/docs/webhook-event-reference). Obtain an OAuth token with the required resource access and ownership permissions. Expose a publicly reachable HTTPS receiver and generate a unique signing secret for each registration. Configure the [receiver](https://developer.webex.com/docs/receive-and-verify-webhooks) before triggering test events.

For message notifications, the token needs `spark:messages_read`. Membership notifications require `spark:memberships_read`. See [Scopes](https://developer.webex.com/docs/integrations#scopes) for application scope selection. Other resources and organization-level registrations have their own requirements below and in the resource API reference.

For Calling resources, check the [interest registration prerequisites](https://developer.webex.com/docs/call-control#interest-registration). Some resource or actor categories require an interest registration in addition to a webhook; interests expire and must be refreshed. These registrations affect applicable webhooks across the organization.
