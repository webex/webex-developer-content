---
type: Guide
title: Webex Webhooks API | Register and manage webhooks
display_title: Register and manage webhooks
canonical_url: https://developer.webex.com/docs/register-and-manage-webhooks
content_type: documentation
product_group:
- webex-suite
categories:
- admin
- calling
- create
- meeting
- messaging
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/register-and-manage-webhooks)

Register Webex Webhooks API notifications for Messaging, Meetings, Calling, and platform events, then manage registrations owned by your application.

## Before you begin

This page covers `/v1/webhooks`. Contact Center event subscriptions use a [different registration guide](https://developer.webex.com/docs/using-webhooks). A Contact Center application still uses this guide when subscribing to platform Service App authorization events.

Choose a resource and event from the [event reference](https://developer.webex.com/docs/webhook-event-reference). Obtain an OAuth token with the required resource access and ownership permissions. Expose a publicly reachable HTTPS receiver and generate a unique signing secret for each registration. Configure the [receiver](https://developer.webex.com/docs/receive-and-verify-webhooks) before triggering test events.

For message notifications, the token needs `spark:messages_read`. Membership notifications require `spark:memberships_read`. See [Scopes](https://developer.webex.com/docs/integrations#scopes) for application scope selection. Other resources and organization-level registrations have their own requirements below and in the resource API reference.

For Calling resources, check the [interest registration prerequisites](https://developer.webex.com/docs/call-control#interest-registration). Some resource or actor categories require an interest registration in addition to a webhook; interests expire and must be refreshed. These registrations affect applicable webhooks across the organization.

## Org/Admin/Compliance Officer level webhooks

Admins/Compliance Officers often want to have an org wide view of meeting events. Admins registered in Control Hub with the Full admin role have the capability to register webhooks for their org by setting an additional field `ownedBy` with the value set to `org`. Compliance officers can also register webhooks for their org by setting the value of `ownedBy` field with the value set to `org`. Both can filter to specific sites in the org or specific hosts by using the corresponding filter parameters described below.
To register for meeting events at Org level, the Org admin should also be a Webex site admin managing the relevant Webex sites or a Compliance officer for the organization. Integrations acting on-behalf of an admin need to have the Admin level scope to register org wide webhooks.



> **Webhook Disabled When Creator No Longer Exists**
>
> If a webhook was created by a user who has since been deleted or no longer exists in the organization, the webhook will be automatically disabled. This is expected behavior.



## Choosing applications vs serviceApp webhooks

Use the `applications` webhook resource when you need org-wide notifications that a Bot, Integration, or Service App in your organization was created, updated, or deleted. Use the `serviceApp` resource when you need notifications that a Service App was authorized or deauthorized by an administrator. Use `spark:applications_webhook_write` on the token that creates the webhook. The API also accepts `application:webhooks_write` or `spark:all`. Select the webhook scope on the Integration or Service App that calls Create Webhook.

| Dimension              | `serviceApp`                               | `applications`                                                         |
| ---------------------- | ------------------------------------------ | ---------------------------------------------------------------------- |
| Purpose                | Service app authorization lifecycle        | Application CRUD lifecycle (Bots, Integrations, Service Apps)          |
| Events                 | `authorized`, `deauthorized`               | `created`, `updated`, `deleted`                                        |
| Typical subscriber     | User-level token with `spark:applications_webhook_write`, `application:webhooks_write`, or `spark:all`. | Org admin only (`ownedBy: "org"`)                                      |
| Filters                | Supported                                  | None                                                                   |
| Feature availability   | Generally available                        | May require org enablement; see prerequisites below                    |



> **Applications webhook prerequisites**
>
> To register `applications` webhooks you must be an organization administrator with the Full admin role (`id_full_admin`). Your OAuth token must include either `spark:applications_webhook_write` or `application:webhooks_write`. Set `ownedBy` to `org` on the create request—user-level webhooks are not supported for this resource. This capability may not be available in all organizations yet; if webhook creation fails with `invalid field: resource`, contact [Webex developer support](https://developer.webex.com/support) to confirm availability for your organization.





> **Info**
>
> Applications webhooks are documented for commercial Webex environments. FedRAMP (Webex for Government) support is not confirmed—contact [Webex developer support](https://developer.webex.com/support) before building for government deployments.



## User Level Scopes for Meeting Related Webhooks

The following scopes are required to create, get, list, update or delete webhooks at user level for meeting related resources:



| Scope                    | Resource         | Usage                                                                  |
|---------------------------|---------------------|------------------------------------------------------------------------|
| `meeting:schedules_read`    | `meetings`            | Manipulate webhooks of `meetings` resource as a normal user            |
| `meeting:participants_read` | `meetingParticipants` | Manipulate webhooks of `meetingParticipants` resource as a normal user |
| `meeting:recordings_read`   | `recordings`          | Manipulate webhooks of `recordings` resource as a normal user          |
| `meeting:transcripts_read`  | `meetingTranscripts`  | Manipulate webhooks of `meetingTranscripts` resource as a normal user  |
## Organization/Admin/Compliance Officer Level Scopes for Meeting Related Webhooks

The following scopes are required to create, get, list, update or delete webhooks at organization level for meeting related resources:



| Scope                          | Resource                      | Usage                                                                                         |
|---------------------------------|--------------------------------|-----------------------------------------------------------------------------------------------|
| `meeting:admin_schedule_read`     | `meetings`                       | Manipulate webhooks of `meetings` resource as an admin                                        |
| `meeting:admin_participants_read` | `meetingParticipants`            | Manipulate webhooks of `meetingParticipants` resource as an admin                             |
| `meeting:admin_recordings_read`   | `recordings`                     | Manipulate webhooks of `recordings` resource as an admin                                      |
| `meeting:admin_transcripts_read`  | `meetingTranscripts`             | Manipulate webhooks of `meetingTranscripts` resource as an admin                              |
| `spark-compliance:meetings_read`  | `recordings, meetingTranscripts` | Manipulate webhooks of `recordings` and `meetingTranscripts` resource as a compliance officer |

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



## Creating a Webhook

To begin receiving platform events, you first need to register a webhook with Webex. To create a webhook, make an HTTP POST to `/webhooks` with some basic information as shown in the example below:

```json
{
  "name": "New message in 'Project Unicorn' room",
  "targetUrl": "https://example.com/spark-hook",
  "resource": "messages",
  "event": "created",
  "filter": "roomId=Y2lzY29zcGFyazovL3VzL1JPT00vYmJjZWIxYWQtNDNmMS0zYjU4LTkxNDctZjE0YmIwYzRkMTU0"
}
```

<a id="request-parameters"></a>

### Request Parameters



| Parameter   | Explanation                                                                                                                                                                                                                                                                                                                              |
| ----------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `name`      | A label to remember why it was created. Use it for whatever purpose you'd like.                                                                                                                                                                                                                                                          |
| `targetUrl` | Tell Webex where you'd like to receive platform events. See the following [Handling Requests from Webex](https://developer.webex.com/docs/receive-and-verify-webhooks#handling-requests-from-webex) section for detailed information about the webhook request format and best practices for scaling your infrastructure.                                                                |
| `resource`  | Indicates the noun being observed and will generally match the plural form of one of the Webex APIs (i.e. messages).                                                                                                                                                                                                               |
| `event`     | Further narrows the events by specifying the action that would trigger a notification to your backend.                                                                                                                                                                                                                                   |
| `filter`    | A set of filtering critera. Generally speaking, webhook filters will be a subset of the query parameters available when GETing a list of the target resource. It is an optional property. To add multiple filters, separate them with the “&” symbol. For more information about filters, see [Filtering Webhooks](https://developer.webex.com/docs/register-and-manage-webhooks#filtering-webhooks). |
| `secret`    | A shared secret used to sign webhook payloads. This API field is optional, but set a unique secret for each webhook and verify signatures before processing. See [Authenticating Requests](https://developer.webex.com/docs/receive-and-verify-webhooks#authenticating-requests).                                                                                                                                                                                                              |

A valid OAuth token is required to create a webhook. An existing webhook can continue sending notifications after the token used to register it expires, provided your endpoint acknowledges deliveries successfully. Payload contents vary by resource; for example, `applications` updates include an application lifecycle snapshot. Treat every delivery as sensitive: use HTTPS for the target URL, set a unique secret, and verify the signature over the raw request body before logging or processing the payload. See [Authenticating Requests](https://developer.webex.com/docs/receive-and-verify-webhooks#authenticating-requests) for details.

<a id="applications-webhook-examples"></a>

### Applications webhook examples

Register a separate webhook for each event you want to receive (`created`, `updated`, or `deleted`). Omit the `filter` field—filters are not supported for `applications` webhooks. Generate a different high-entropy secret for each registration, store it in a secret manager, and substitute that value for the illustrative `secret` strings below before making the API request. Verify each delivery signature before processing it.

**Created** — notify when an application is added to the organization:

```json
{
  "name": "Org applications created",
  "targetUrl": "https://example.com/webhooks/applications-created",
  "resource": "applications",
  "event": "created",
  "secret": "<unique-secret-from-secret-manager>",
  "ownedBy": "org"
}
```

**Updated** — notify when an application is modified (payload includes an application lifecycle snapshot):

```json
{
  "name": "Org applications updated",
  "targetUrl": "https://example.com/webhooks/applications-updated",
  "resource": "applications",
  "event": "updated",
  "secret": "<unique-secret-from-secret-manager>",
  "ownedBy": "org"
}
```

**Deleted** — notify when an application is removed:

```json
{
  "name": "Org applications deleted",
  "targetUrl": "https://example.com/webhooks/applications-deleted",
  "resource": "applications",
  "event": "deleted",
  "secret": "<unique-secret-from-secret-manager>",
  "ownedBy": "org"
}
```

Verify `applications` deliveries using the [receiver guide](https://developer.webex.com/docs/receive-and-verify-webhooks). It owns signature verification, acknowledgement, and retry handling.

For `updated` events, `data` contains an application lifecycle snapshot. Compare its [documented fields](https://developer.webex.com/docs/webhook-event-reference#interpret-payloads) with your stored state to identify changes. Do not assume the snapshot matches the complete response of an application details API.

Organizations with federated identity may experience additional webhook delivery latency.

<a id="troubleshooting-applications-webhooks"></a>

### Troubleshooting applications webhooks

| Error or symptom | Likely cause | What to do |
| ---------------- | ------------ | ---------- |
| `invalid field: resource` | The `applications` webhook resource is not available for your organization yet, or the request body uses an unsupported resource value. | Confirm org enablement with [Webex developer support](https://developer.webex.com/support). Verify `resource` is exactly `applications`. |
| `403 Forbidden` | Missing org admin role or required OAuth scope. | Use a token for a Full admin (`id_full_admin`) with either `spark:applications_webhook_write` or `application:webhooks_write`. |
| Invalid event for resource | Events such as `authorized` or `deauthorized` belong to the `serviceApp` resource, not `applications`. | Use `created`, `updated`, or `deleted` for `applications`. See [Choosing applications vs serviceApp webhooks](#choosing-applications-vs-serviceapp-webhooks). |
| Authorization failure without `ownedBy: "org"` | `applications` webhooks require org-level registration. | Set `"ownedBy": "org"` on the create request. |
| `invalid value for filter` (or similar) | Filters are not supported for `applications`. | Remove the `filter` field or leave it empty. |
| Expected a field diff on `updated` | `updated` notifications include a lifecycle snapshot. | Compare the documented [snapshot fields](https://developer.webex.com/docs/webhook-event-reference#interpret-payloads) with your stored state; it is not a field-level diff. |

## Complete registration request

Send the following request with your own access token, test space ID, HTTPS destination, and unique signing secret. The placeholders are illustrative; do not send them literally.

```http
POST https://webexapis.com/v1/webhooks
Authorization: Bearer <access-token>
Content-Type: application/json

{
  "name": "Test message created",
  "targetUrl": "https://example.com/webhooks/messages",
  "resource": "messages",
  "event": "created",
  "filter": "roomId=<test-room-id>",
  "secret": "<unique-secret-from-secret-manager>"
}
```

## Receive your first event

1. Select a test Webex space your token can access and obtain its room ID with [List Rooms](https://developer.webex.com/docs/api/v1/rooms/list-rooms).
2. Use [Create a Webhook](https://developer.webex.com/docs/api/v1/webhooks/create-a-webhook) with `resource: messages`, `event: created`, `filter: roomId=<test-room-id>`, your HTTPS `targetUrl`, and a unique `secret`. Store the returned registration ID and its secret together. Add the `secret` to the message example above before submitting it.
3. Post a message in that space. Expect a delivery with `resource: messages`, `event: created`, and a `data.id` identifying the message.
4. Verify the delivery signature over its original bytes. Accept the event durably before acknowledging it, then fetch message content with your application token if needed. See [Receive and verify events](https://developer.webex.com/docs/receive-and-verify-webhooks).
5. Inspect the registration with [Get Webhook Details](https://developer.webex.com/docs/api/v1/webhooks/get-webhook-details). The envelope `id` should match this registration, not the individual message.
6. Delete only this test registration with [Delete a Webhook](https://developer.webex.com/docs/api/v1/webhooks/delete-a-webhook).

<a id="webex-webhooks"></a>

## Manage registration lifecycle

| Task or change | Action |
| --- | --- |
| Inspect or enumerate your registrations | Use [Get Webhook Details](https://developer.webex.com/docs/api/v1/webhooks/get-webhook-details) or [List Webhooks](https://developer.webex.com/docs/api/v1/webhooks/list-webhooks). |
| Change supported registration fields | Use [Update a Webhook](https://developer.webex.com/docs/api/v1/webhooks/update-a-webhook); consult that operation for mutable fields. |
| Remove a registration | Delete only registrations your application owns. Keep ownership records so cleanup cannot remove another integration's webhook. |
| Registration token expires | Existing delivery can continue; authenticated API calls still require a valid token. |
| Creator is deleted | The existing guide documents automatic disablement. Monitor registration status and follow the [recovery instructions](https://developer.webex.com/docs/receive-and-verify-webhooks#disabled-webhooks). |
| Calling interest expires | Refresh the applicable [interest registration](https://developer.webex.com/docs/call-control#interest-registration). A webhook registration alone does not enable every Calling event. |

Registration limits depend on ownership, resources, and filters. Wildcard registrations can count as several resource/event registrations. Organization-owned duplicate checks also distinguish the application, resource, event, and filter; do not interpret the limit as one webhook for an entire organization. Consult the API reference and confirm the applicable limit with developer support before designing high-volume provisioning.
