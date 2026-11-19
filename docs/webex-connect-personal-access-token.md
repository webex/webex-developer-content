---
type: Guide
title: Webex Connect Personal Access Token
display_title: Personal Access Token
canonical_url: https://developer.webex.com/docs/webex-connect-personal-access-token
content_type: documentation
product_group:
- webex-connect
categories:
- webex-connect
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/webex-connect-personal-access-token)

Use a Webex personal access token to call the digital asset APIs with your own user identity.

## Before you begin

Your Webex account must be associated with the Webex Connect organization whose assets you want to manage. Your user must also have the required asset-management permission.

The token must include the scope required by the Email, Live Chat, or In-App operation. A scope allows the API operation, but it does not override the user's organization access or role.

## Get your token

1. Sign in to the Webex Developer Portal with the account associated with your Webex Connect organization.
2. Open a Webex Connect digital asset operation in the API Reference.
3. Select **Use personal access token** in the **Try Out** panel.
4. Copy the token for use in your development request.

Personal access tokens are short-lived and intended for development and testing. Generate a current token when an earlier token expires.

## Use the token

Pass the token in the `Authorization` header:

```bash
curl --request GET \
  --url '<digital-asset-api-base-url>/<resource-path>' \
  --header 'Authorization: Bearer <personal-access-token>' \
  --header 'x-organization-id: <organization-id>' \
  --header 'Accept: application/json'
```

## If the request is rejected

- For `401 Unauthorized`, obtain a current token and verify the bearer header.
- For `403 Forbidden`, verify the required asset scope, organization access, and user permission.
- Confirm that `x-organization-id` identifies the organization associated with your account.
- Confirm that the operation supports the requested asset type.

## Protect your token

Do not embed a personal access token in client-side code, commit it to source control, include it in screenshots, or send it in a support request. Remove the `Authorization` header from logs before sharing them.
