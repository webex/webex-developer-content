---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-connect-personal-access-token
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Use the token
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webex-connect-personal-access-token). [Full Markdown](../../../../docs/webex-connect-personal-access-token.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md)

## Article introduction

Use a Webex personal access token to call the digital asset APIs with your own user identity.

## Selected section

## Use the token

Pass the token in the `Authorization` header:

```bash
curl --request GET \
  --url '<digital-asset-api-base-url>/<resource-path>' \
  --header 'Authorization: Bearer <personal-access-token>' \
  --header 'x-organization-id: <organization-id>' \
  --header 'Accept: application/json'
```
