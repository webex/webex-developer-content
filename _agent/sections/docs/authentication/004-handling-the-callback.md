---
type: Excerpt
canonical_url: https://developer.webex.com/docs/authentication
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Handling the callback
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/authentication). [Full Markdown](../../../../docs/authentication.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Why authentication is required](001-why-authentication-is-required.md) [Before you implement OAuth](002-before-you-implement-oauth.md) [Requesting Permission](003-requesting-permission.md)

## Article introduction

Webex authentication lets your integration securely access Webex APIs on behalf of a user without collecting or storing their Webex password.

## Selected section

## Handling the callback

After the user approves access, Webex redirects the browser to the registered `redirect_uri`. The callback includes the one-time authorization code and the state value, for example:

`https://your-server.example.com/auth?code=AUTHORIZATION_CODE&state=STATE_VALUE`

Verify `state` before using `code`. The authorization code is short-lived and can be exchanged only once.
