---
type: Excerpt
canonical_url: https://developer.webex.com/docs/become-a-byova-provider
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Handle deauthorization and offboarding
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/become-a-byova-provider). [Full Markdown](../../../../docs/become-a-byova-provider.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](002-before-you-begin.md)

## Article introduction

Build and operate a Webex App Hub Service App that securely connects your virtual agent gateway to each customer's Webex Contact Center organization.

## Selected section

## Handle deauthorization and offboarding

When Webex sends a [`serviceApp.deauthorized`
event](https://developer.webex.com/docs/webhooks), first verify the signature over the
unmodified raw request body. Before offboarding, require the expected resource
and event, confirm that `data.id` equals the expected Service App ID, and
verify that `data.authorizerOrgId` maps to an active onboarding record. Then:

1. Disable the organization route at your gateway immediately.
1. Mark the datasource and onboarding record inactive.
1. Remove or cryptographically erase stored organization tokens.
1. Tell the customer to remove or redirect the related Virtual Agent feature
   and flow.
1. Retain only the minimum audit information your support and compliance
   requirements need.

Do not allow a stale or deauthorized organization to continue using your
gateway.
