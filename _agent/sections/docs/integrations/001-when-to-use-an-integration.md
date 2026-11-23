---
type: Excerpt
canonical_url: https://developer.webex.com/docs/integrations
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- When to use an integration
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/integrations). [Full Markdown](../../../../docs/integrations.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Webex Contact Center requirements](003-webex-contact-center-requirements.md) [Scopes](004-scopes.md)

## Article introduction

Create a Webex integration when your application needs a user to authorize access to Webex APIs on their behalf.

[Create an Integration](<https://developer.webex.com/my-apps/new/integration>)

## Selected section

## When to use an integration

An integration is an OAuth 2.0 client registered with Webex. It receives a temporary access token after a Webex user signs in and approves the requested scopes. Use an integration for applications that act on behalf of a user and can send that user through an interactive authorization flow.

You don't need to register an integration to explore the APIs with your own [personal access token](https://developer.webex.com/docs/getting-your-personal-access-token).

For unattended, organization-wide automation that should not depend on a user's lifecycle, use a Service App. Webex Contact Center developers should see [Contact Center Service Apps](https://developer.webex.com/webex-contact-center/docs/contact-center-service-apps).
