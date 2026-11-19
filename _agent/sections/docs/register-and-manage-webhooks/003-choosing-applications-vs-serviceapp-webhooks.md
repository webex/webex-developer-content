---
type: Excerpt
canonical_url: https://developer.webex.com/docs/register-and-manage-webhooks
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Choosing applications vs serviceApp webhooks
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/register-and-manage-webhooks). [Full Markdown](../../../../docs/register-and-manage-webhooks.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md) [User Level Scopes for Meeting Related Webhooks](004-user-level-scopes-for-meeting-related-webhooks.md) [Organization/Admin/Compliance Officer Level Scopes for Meeting Related Webhooks](005-organization-admin-compliance-officer-level-scopes-for-meeti.md)

## Article introduction

Register Webex Webhooks API notifications for Messaging, Meetings, Calling, and platform events, then manage registrations owned by your application.

## Selected section

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
