---
type: Excerpt
canonical_url: https://developer.webex.com/docs/manage-your-published-app
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Plan retirement and customer offboarding
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/manage-your-published-app). [Full Markdown](../../../../docs/manage-your-published-app.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Plan application and permission changes](003-plan-application-and-permission-changes.md)

## Article introduction

Keep your App Hub listing accurate, support customers through changes, and plan updates or retirement alongside the authorization lifecycle of your app.

## Selected section

## Plan retirement and customer offboarding

Plan the customer transition before stopping the service:

1. Identify affected customers, dependencies, and any data export or deletion work required by your commitments to them.
2. Communicate the planned end of service, any replacement, required customer actions, and the support path.
3. Coordinate the App Hub listing change or removal with the review team through your existing correspondence or [Developer Support](https://developer.webex.com/support).
4. Complete the deauthorization, deprovisioning, and data-handling steps for your app type.
5. Verify that your application no longer performs work for offboarded customers and that their provisioning state reflects the change.

Listing removal, Webex authorization, and your own service's customer state are separate concerns. Confirm each explicitly rather than assuming that removing a listing revokes credentials or deletes customer data.

For Service Apps, use [Deauthorizing a Service App](https://developer.webex.com/docs/service-apps#deauthorizing-a-service-app). For BYOVA, use the provider guide's [offboarding procedure](https://developer.webex.com/docs/become-a-byova-provider#handle-deauthorization-and-offboarding). Follow the applicable product guide for other app types.
