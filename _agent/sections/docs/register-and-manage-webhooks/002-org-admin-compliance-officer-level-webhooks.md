---
type: Excerpt
canonical_url: https://developer.webex.com/docs/register-and-manage-webhooks
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Org/Admin/Compliance Officer level webhooks
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/register-and-manage-webhooks). [Full Markdown](../../../../docs/register-and-manage-webhooks.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md) [User Level Scopes for Meeting Related Webhooks](004-user-level-scopes-for-meeting-related-webhooks.md) [Organization/Admin/Compliance Officer Level Scopes for Meeting Related Webhooks](005-organization-admin-compliance-officer-level-scopes-for-meeti.md)

## Article introduction

Register Webex Webhooks API notifications for Messaging, Meetings, Calling, and platform events, then manage registrations owned by your application.

## Selected section

## Org/Admin/Compliance Officer level webhooks

Admins/Compliance Officers often want to have an org wide view of meeting events. Admins registered in Control Hub with the Full admin role have the capability to register webhooks for their org by setting an additional field `ownedBy` with the value set to `org`. Compliance officers can also register webhooks for their org by setting the value of `ownedBy` field with the value set to `org`. Both can filter to specific sites in the org or specific hosts by using the corresponding filter parameters described below.
To register for meeting events at Org level, the Org admin should also be a Webex site admin managing the relevant Webex sites or a Compliance officer for the organization. Integrations acting on-behalf of an admin need to have the Admin level scope to register org wide webhooks.



> **Webhook Disabled When Creator No Longer Exists**
>
> If a webhook was created by a user who has since been deleted or no longer exists in the organization, the webhook will be automatically disabled. This is expected behavior.
