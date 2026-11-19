---
type: Excerpt
canonical_url: https://developer.webex.com/docs/authentication
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Why authentication is required
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/authentication). [Full Markdown](../../../../docs/authentication.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you implement OAuth](002-before-you-implement-oauth.md) [Requesting Permission](003-requesting-permission.md)

## Article introduction

Webex authentication lets your integration securely access Webex APIs on behalf of a user without collecting or storing their Webex password.

## Selected section

## Why authentication is required

Webex APIs protect user and organization data. Before an integration can read that data or perform an action, Webex must confirm who is granting access and what the integration is allowed to do.

The OAuth 2.0 authorization code flow provides that consent and establishes a secure way for your integration to make API requests:

1. Your integration sends the user to Webex to sign in.
2. Webex shows the user the permissions, or scopes, that your integration is requesting.
3. The user approves or denies access.
4. If access is approved, Webex sends your application a short-lived authorization code.
5. Your server exchanges the code for an access token and refresh token.
6. Your integration uses the access token when calling Webex APIs and the refresh token when continued access is needed.

The access token represents the user and the permissions they approved. It does not give the integration unrestricted access: the token is limited by its scopes and by the permissions of the user who authorized it.

For quick API exploration, you can use your own [personal access token](https://developer.webex.com/docs/getting-your-personal-access-token). Register an OAuth integration when an application needs to access Webex for other users or maintain access beyond a personal token's lifetime.
