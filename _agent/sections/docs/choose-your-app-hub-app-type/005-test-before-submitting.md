---
type: Excerpt
canonical_url: https://developer.webex.com/docs/choose-your-app-hub-app-type
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Test before submitting
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/choose-your-app-hub-app-type). [Full Markdown](../../../../docs/choose-your-app-hub-app-type.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Match listing and authorization to your app](003-match-listing-and-authorization-to-your-app.md)

## Article introduction

Choose the Webex app type that fits your customer workflow, then follow its development and App Hub submission guidance.

## Selected section

## Test before submitting

Choose a sandbox for the product your app supports:

- **Webex Suite:** Use the [Suite Sandbox](https://developer.webex.com/app-hub/docs/developer-sandbox-guide) for supported collaboration workflows.
- **Webex Contact Center:** Use the [Contact Center Sandbox](https://developer.webex.com/app-hub/docs/sandbox_cc) guide to set up a licensed Contact Center test environment with administrator access and preconfigured resources. For virtual agent solutions, also confirm the prerequisites in the [BYOVA provider guide](https://developer.webex.com/app-hub/docs/become-a-byova-provider).

Check the selected sandbox's prerequisites and available features; a sandbox does not establish that every API or app type is available.

Verify the complete customer journey:

1. A new customer can understand what the app does and what accounts or licenses it requires.
2. The intended user or administrator can authorize it with only the permissions it needs.
3. The main workflow works in each supported Webex context.
4. Denied access, expired credentials, and interrupted setup produce a useful recovery path.
5. Customers can stop using the app and follow the applicable deauthorization or removal procedure.

Use separate test identities where the workflow has different roles. A successful test inside your own organization does not prove that authorization in an unrelated customer organization is ready.
