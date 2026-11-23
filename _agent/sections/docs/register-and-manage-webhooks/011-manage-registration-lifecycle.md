---
type: Excerpt
canonical_url: https://developer.webex.com/docs/register-and-manage-webhooks
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Manage registration lifecycle
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/register-and-manage-webhooks). [Full Markdown](../../../../docs/register-and-manage-webhooks.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md) [User Level Scopes for Meeting Related Webhooks](004-user-level-scopes-for-meeting-related-webhooks.md) [Organization/Admin/Compliance Officer Level Scopes for Meeting Related Webhooks](005-organization-admin-compliance-officer-level-scopes-for-meeti.md)

## Article introduction

Register Webex Webhooks API notifications for Messaging, Meetings, Calling, and platform events, then manage registrations owned by your application.

## Selected section

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
