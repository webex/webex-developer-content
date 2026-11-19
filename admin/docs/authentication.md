---
type: Guide
title: Authentication
display_title: Authentication
canonical_url: https://developer.webex.com/docs/authentication
content_type: documentation
product_group:
- webex-suite
- webex-contact-center
categories:
- admin
- calling
- create
- meeting
- messaging
- webex-contact-center
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/authentication)

Webex authentication lets your integration securely access Webex APIs on behalf of a user without collecting or storing their Webex password.

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

## Before you implement OAuth

To implement the OAuth flow described below, you need:

- A registered [Webex integration](https://developer.webex.com/docs/integrations) and its client ID and client secret.
- A redirect URI that exactly matches one of the URIs registered for the integration.
- The minimum [integration scopes](https://developer.webex.com/docs/integration-scopes) required by your application.
- A server that can receive the OAuth callback and protect the client secret and tokens.

For Webex Contact Center administrator APIs, the user authorizing the integration must use a Webex account backed by Cisco Webex Common Identity and have the appropriate administrator role in Control Hub. See [Webex Contact Center administrator roles and privileges](https://help.webex.com/en-us/article/n5jdj19/Webex-Contact-Center-administrator-roles-and-privileges).

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

## Handling the callback

After the user approves access, Webex redirects the browser to the registered `redirect_uri`. The callback includes the one-time authorization code and the state value, for example:

`https://your-server.example.com/auth?code=AUTHORIZATION_CODE&state=STATE_VALUE`

Verify `state` before using `code`. The authorization code is short-lived and can be exchanged only once.

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

## Invoking the Webex APIs

Send the access token in the `Authorization` header using the Bearer scheme:

```bash
curl 'https://webexapis.com/v1/people/me' \
  --header 'Authorization: Bearer YOUR_ACCESS_TOKEN' \
  --header 'Accept: application/json'
```

For Authorization Code Flow with Proof Key for Code Exchange (PKCE), Device Authorization Grant, and OpenID Connect behavior, see [Login with Webex](https://developer.webex.com/docs/login-with-webex).

## Next steps

- To test Webex APIs with your own account, get a [Personal Access Token](https://developer.webex.com/docs/getting-your-personal-access-token).
- To access Webex on behalf of other users, [create an Integration](https://developer.webex.com/docs/integrations) and review the available [Integration Scopes](https://developer.webex.com/docs/integration-scopes).
