---
type: Excerpt
canonical_url: https://developer.webex.com/docs/app-hub-build-and-test
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Build a small working version
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/app-hub-build-and-test). [Full Markdown](../../../../docs/app-hub-build-and-test.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Continue to submission and customer setup](006-continue-to-submission-and-customer-setup.md)

## Article introduction

Turn your chosen app type into a working customer workflow. Plan the components and permissions, build a small working version, and test setup, everyday use, and recovery before preparing your App Hub submission.

## Selected section

## Build a small working version

Work through the selected implementation guide in this order:

1. **Prepare the environment.** Confirm the required products and roles, set up your application or service, and register the components the workflow needs.
2. **Implement authorization.** Use the documented flow for each component and request only the scopes needed for the first workflow. Keep client secrets and refresh tokens on your backend, and exclude credentials from logs.
3. **Connect one real operation.** Replace sample or placeholder behavior with the intended API call, interaction, or conversation. Verify the result in the target Webex context.
4. **Add recovery.** Make denied access, missing prerequisites, expired access, and interrupted setup understandable. Follow the guide for your app type for token renewal and authorization changes.

Keep customer connections separate in your service. When handling a request or event, verify that it uses the intended customer's authorization and resources. If the workflow processes asynchronous events, design retries so they do not repeat an unintended customer action.
