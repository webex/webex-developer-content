---
type: Excerpt
canonical_url: https://developer.webex.com/docs/authentication
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Requesting Permission
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/authentication). [Full Markdown](../../../../docs/authentication.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Why authentication is required](001-why-authentication-is-required.md) [Before you implement OAuth](002-before-you-implement-oauth.md)

## Article introduction

Webex authentication lets your integration securely access Webex APIs on behalf of a user without collecting or storing their Webex password.

## Selected section

## Requesting Permission

Send the user to the Webex authorization endpoint:

`https://webexapis.com/v1/authorize`

Include these URL-encoded query parameters:



| Query parameter | Value |
| --- | --- |
| `response_type` | Set to `code`. |
| `client_id` | The client ID issued when you created the integration. |
| `redirect_uri` | One of the redirect URIs registered for the integration. |
| `scope` | A space-separated list of scopes registered for the integration. |
| `state` | A unique value your application can validate when Webex calls the redirect URI. |

After the user signs in, Webex displays a grant dialog showing the access requested by the integration.

![OAuth app grant dialog](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt97d451f588b09709/5b1014bc344ad0d40f7812eb/authentication-app_grant.png)

### Scopes

Scopes limit the resources and operations available to an access token. Request only the scopes your application needs and ensure that the authorizing user has the corresponding permissions. See [Integration Scopes](https://developer.webex.com/docs/integration-scopes) for the complete list and important scope behavior.

### State

Use the `state` parameter to correlate the callback with the authorization request and protect against request tampering. Generate an unpredictable value for each authorization attempt, associate it with the user's session, and validate the returned value before exchanging the authorization code.
