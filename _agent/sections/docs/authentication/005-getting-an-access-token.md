---
type: Excerpt
canonical_url: https://developer.webex.com/docs/authentication
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Getting an Access Token
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/authentication). [Full Markdown](../../../../docs/authentication.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Why authentication is required](001-why-authentication-is-required.md) [Before you implement OAuth](002-before-you-implement-oauth.md) [Requesting Permission](003-requesting-permission.md)

## Article introduction

Webex authentication lets your integration securely access Webex APIs on behalf of a user without collecting or storing their Webex password.

## Selected section

## Getting an Access Token

Exchange the authorization code by sending an `application/x-www-form-urlencoded` POST request to:

`https://webexapis.com/v1/access_token`

Include these parameters:



| Parameter | Value |
| --- | --- |
| `grant_type` | Set to `authorization_code`. |
| `client_id` | The integration's client ID. |
| `client_secret` | The integration's client secret. |
| `code` | The authorization code returned to the redirect URI. |
| `redirect_uri` | The same redirect URI used in the authorization request. |

```bash
curl --request POST 'https://webexapis.com/v1/access_token' \
  --header 'Content-Type: application/x-www-form-urlencoded' \
  --data-urlencode 'grant_type=authorization_code' \
  --data-urlencode 'client_id=YOUR_CLIENT_ID' \
  --data-urlencode 'client_secret=YOUR_CLIENT_SECRET' \
  --data-urlencode 'redirect_uri=https://your-server.example.com/auth' \
  --data-urlencode 'code=AUTHORIZATION_CODE'
```

The response contains an access token, a refresh token, and their expiration values. Store the tokens securely and use the expiration values returned by the service rather than assuming a fixed lifetime.

### Using the Refresh Token

Before continued access is needed, exchange the refresh token for a new access token by sending another form-encoded POST request to `https://webexapis.com/v1/access_token`.

| Parameter | Value |
| --- | --- |
| `grant_type` | Set to `refresh_token`. |
| `client_id` | The integration's client ID. |
| `client_secret` | The integration's client secret. |
| `refresh_token` | The refresh token returned by the previous token response. |

```bash
curl --request POST 'https://webexapis.com/v1/access_token' \
  --header 'Content-Type: application/x-www-form-urlencoded' \
  --data-urlencode 'grant_type=refresh_token' \
  --data-urlencode 'client_id=YOUR_CLIENT_ID' \
  --data-urlencode 'client_secret=YOUR_CLIENT_SECRET' \
  --data-urlencode 'refresh_token=YOUR_REFRESH_TOKEN'
```

Store the new access token and any replacement refresh token returned by the service.
