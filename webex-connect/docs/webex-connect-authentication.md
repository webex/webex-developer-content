---
type: Guide
title: Webex Connect API Authentication
display_title: Authentication
canonical_url: https://developer.webex.com/docs/webex-connect-authentication
content_type: documentation
product_group:
- webex-connect
categories:
- webex-connect
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/webex-connect-authentication)

Use a Webex personal access token to authenticate requests to the digital asset APIs for Email and Chat assets. Chat assets support Push Notifications, Live Chat, and In-App Messaging.

## How access is evaluated

Authentication verifies the token and identifies the Webex user. Authorization then verifies that:

- The token contains the scope required for the digital asset operation.
- The user can access the organization identified by `x-organization-id`.
- The user has permission to manage the requested asset.

The required token scope permits the API operation; it does not grant organization access or a higher administrative role.

## Send the personal access token

Include the token in each request to a digital asset API using the bearer scheme:

```http
Authorization: Bearer <personal-access-token>
```

Do not send the token as a query parameter or in the request body.

## Identify the organization

Include the organization ID in the `x-organization-id` header. The organization must be associated with the user represented by the token.

```http
x-organization-id: <organization-id>
```

## Use a personal access token

Use a personal access token to explore operations in **Try Out**, verify permissions and request formats, and develop against the Email and Chat digital asset APIs. For steps to get a token, see [Personal Access Token](https://developer.webex.com/webex-connect/docs/webex-connect-personal-access-token).

The required scope is documented for each API operation in the [Digital Asset API Reference](https://developer.webex.com/webex-connect/docs/api/v1/webex-connect-email-digital-asset-apis-email-channel/create-an-email-asset). Other Webex Connect API families may use different authentication methods; see [API Authentication and IP Allowlisting](https://developers.webexconnect.io/reference/api-authentication).

## Protect the token

- Do not commit personal access tokens to source control.
- Do not include personal access tokens in browser code, screenshots, or support tickets.
- Remove the `Authorization` header and token values from application logs.
- Obtain a new token after the current token expires.
- Request only the scopes needed for the asset operations you are testing.
