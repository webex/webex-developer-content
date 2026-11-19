---
type: Excerpt
canonical_url: https://developer.webex.com/docs/register-and-manage-webhooks
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Creating a Webhook
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/register-and-manage-webhooks). [Full Markdown](../../../../docs/register-and-manage-webhooks.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md) [User Level Scopes for Meeting Related Webhooks](004-user-level-scopes-for-meeting-related-webhooks.md) [Organization/Admin/Compliance Officer Level Scopes for Meeting Related Webhooks](005-organization-admin-compliance-officer-level-scopes-for-meeti.md)

## Article introduction

Register Webex Webhooks API notifications for Messaging, Meetings, Calling, and platform events, then manage registrations owned by your application.

## Selected section

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
| Invalid event for resource | Events such as `authorized` or `deauthorized` belong to the `serviceApp` resource, not `applications`. | Use `created`, `updated`, or `deleted` for `applications`. See [Choosing applications vs serviceApp webhooks](https://developer.webex.com/docs/register-and-manage-webhooks#choosing-applications-vs-serviceapp-webhooks). |
| Authorization failure without `ownedBy: "org"` | `applications` webhooks require org-level registration. | Set `"ownedBy": "org"` on the create request. |
| `invalid value for filter` (or similar) | Filters are not supported for `applications`. | Remove the `filter` field or leave it empty. |
| Expected a field diff on `updated` | `updated` notifications include a lifecycle snapshot. | Compare the documented [snapshot fields](https://developer.webex.com/docs/webhook-event-reference#interpret-payloads) with your stored state; it is not a field-level diff. |
