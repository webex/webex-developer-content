---
type: Excerpt
canonical_url: https://developer.webex.com/docs/register-and-manage-webhooks
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- The Firehose Webhook
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/register-and-manage-webhooks). [Full Markdown](../../../../docs/register-and-manage-webhooks.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md) [User Level Scopes for Meeting Related Webhooks](004-user-level-scopes-for-meeting-related-webhooks.md) [Organization/Admin/Compliance Officer Level Scopes for Meeting Related Webhooks](005-organization-admin-compliance-officer-level-scopes-for-meeti.md)

## Article introduction

Register Webex Webhooks API notifications for Messaging, Meetings, Calling, and platform events, then manage registrations owned by your application.

## Selected section

## The Firehose Webhook

The Webhooks resource supports what is commonly known as a “firehose” or “wildcard” webhook, which allows your app to subscribe to all events from several commonly-used resources with a single webhook. There are two types of firehoses. One is a “single resource firehose” and the other is an “all resource” firehose.

The event expansion depends on whether you select one resource or `all` resources. An all-resource registration covers `memberships`, `messages`, and `rooms`.

<a id="single-resource-firehose"></a>

### Single Resource Firehose

A single-resource firehose uses `event: "all"` to select the resource’s supported wildcard event set. For example, to subscribe to `all` events for the `messages` resource, your app can create a webhook as shown below:

```json
{
  "name": "Messages Firehose",
  "targetUrl": "https://example.com/message-events",
  "resource": "messages",
  "event": "all"
}
```

For `meetings`, `event: "all"` includes `created`, `updated`, `deleted`, `started`, and `ended`. For `meetingParticipants`, it includes `joined` and `left`. The standard wildcard set for other supported resources is `created`, `updated`, and `deleted`; do not assume `all` includes every specialized event in the reference. Resource permissions and feature availability still apply.

<a id="all-resource-firehose"></a>

### All Resource Firehose

An all resource firehose webhook will send a notification for any event for all supported resource types. The following resources will be included in the “all resource” firehose: memberships, messages, and rooms.

For example, to subscribe to *all* events that occur on *all* supported resources, create a webhook with the resource set to `all` and the event set to `all` as shown below:

```json
{
  "name": "Awesome Bot Webhook Firehose",
  "targetUrl": "https://example.com/spark-events",
  "resource": "all",
  "event": "all"
}
```



> **Warning**
>
> Creating a webhook for `all` resources requires that you have read [scopes](https://developer.webex.com/docs/integrations#scopes) for all supported resources: memberships, messages, and rooms.
