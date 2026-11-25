---
type: Excerpt
canonical_url: https://developer.webex.com/docs/app-hub-customer-onboarding
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Verify the customer journey
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/app-hub-customer-onboarding). [Full Markdown](../../../../docs/app-hub-customer-onboarding.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Match authorization to the app](003-match-authorization-to-the-app.md) [Write the customer setup instructions](004-write-the-customer-setup-instructions.md)

## Article introduction

Help customers connect your App Hub app by separating developer preparation from customer authorization, configuration, and verification.

## Selected section

## Verify the customer journey

Test with the intended customer roles and organization arrangement. Success inside the developer's organization does not establish that authorization in a non-affiliated customer organization works.

Confirm that the customer can authorize the intended app, complete product configuration, and perform the main workflow. Where the app serves multiple organizations, verify that each connection uses the correct customer's authorization and data.

Also test denied authorization, insufficient permissions, expired credentials, and interrupted setup. Show a useful next step and preserve enough non-sensitive context for support. For BYOVA, follow the provider guide's end-to-end call verification, rather than treating authorization as proof that calls will reach the virtual agent.
