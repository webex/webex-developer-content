---
type: Excerpt
canonical_url: https://developer.webex.com/docs/authentication
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Invoking the Webex APIs
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/authentication). [Full Markdown](../../../../docs/authentication.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Why authentication is required](001-why-authentication-is-required.md) [Before you implement OAuth](002-before-you-implement-oauth.md) [Requesting Permission](003-requesting-permission.md)

## Article introduction

Webex authentication lets your integration securely access Webex APIs on behalf of a user without collecting or storing their Webex password.

## Selected section

## Invoking the Webex APIs

Send the access token in the `Authorization` header using the Bearer scheme:

```bash
curl 'https://webexapis.com/v1/people/me' \
  --header 'Authorization: Bearer YOUR_ACCESS_TOKEN' \
  --header 'Accept: application/json'
```

For Authorization Code Flow with Proof Key for Code Exchange (PKCE), Device Authorization Grant, and OpenID Connect behavior, see [Login with Webex](https://developer.webex.com/docs/login-with-webex).
