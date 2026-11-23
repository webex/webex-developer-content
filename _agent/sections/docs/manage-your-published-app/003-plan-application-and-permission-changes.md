---
type: Excerpt
canonical_url: https://developer.webex.com/docs/manage-your-published-app
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Plan application and permission changes
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/manage-your-published-app). [Full Markdown](../../../../docs/manage-your-published-app.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Keep your App Hub listing accurate, support customers through changes, and plan updates or retirement alongside the authorization lifecycle of your app.

## Selected section

## Plan application and permission changes

Before releasing a change, compare it with the behavior and permissions customers previously approved. Treat these as separate work items:

1. **Your application:** Test the new behavior and prepare a recovery or rollback plan.
2. **Your registration and customer authorization:** Follow the app-type guide for configuration, scopes, credentials, and authorization changes. Do not assume existing grants include new permissions.
3. **Your App Hub listing:** Update affected descriptions and customer instructions through the review team. Ask whether the change requires another review before scheduling the release.

These steps can have different owners and completion times. A listing update does not grant API permissions, and an application deployment does not prove that an App Hub update has been reviewed.

Use the relevant guidance:

- [Integrations](https://developer.webex.com/docs/integrations) and [Authentication](https://developer.webex.com/docs/authentication) for user-authorized access.
- [Service Apps](https://developer.webex.com/docs/service-apps) for administrator authorization and organization-specific credentials.
- [Embedded Apps Developer Guide](https://developer.webex.com/docs/embedded-apps-guide) for embedded configuration, privacy, and supported contexts.
- [Workspace Integrations](https://developer.webex.com/docs/workspace-integrations) for workspace integration changes and activation.
- [Admin Approval Guide for Agentic Apps](https://developer.webex.com/docs/admin-approval-guide-for-agentic-apps) for server and tool review, signature changes, and post-approval monitoring.
