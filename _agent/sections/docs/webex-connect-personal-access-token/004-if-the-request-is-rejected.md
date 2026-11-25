---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-connect-personal-access-token
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- If the request is rejected
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webex-connect-personal-access-token). [Full Markdown](../../../../docs/webex-connect-personal-access-token.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md)

## Article introduction

Use a Webex personal access token to call the digital asset APIs with your own user identity.

## Selected section

## If the request is rejected

- For `401 Unauthorized`, obtain a current token and verify the bearer header.
- For `403 Forbidden`, verify the required asset scope, organization access, and user permission.
- Confirm that `x-organization-id` identifies the organization associated with your account.
- Confirm that the operation supports the requested asset type.
