---
type: Guide
title: Getting and Using your Personal Access Token
display_title: Personal Access Token
canonical_url: https://developer.webex.com/docs/getting-your-personal-access-token
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

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/getting-your-personal-access-token)

Learn how to get a personal access token for testing Webex APIs with your own account.

## About personal access tokens

Webex REST API requests must include an API access token in the request's `Authorization` header. The token must have the data access scopes required by the requested resource. In a production app, you create a [Webex Integration](https://developer.webex.com/docs/integrations) and use OAuth to obtain an access token. For testing purposes, however, you can get a personal access token from the Developer Portal to make API calls on your own behalf.

Notes about personal access tokens:

* They should not be used in production apps. Instead, create an [Integration](https://developer.webex.com/docs/integrations) with the desired access scopes to obtain access tokens.
* Personal access tokens are valid for 12 hours after logging into the Developer Portal.

## Get your personal access token

Sign in to the Developer Portal and click the copy icon next to the **Bearer** field below. Click **OK** to copy the token to your clipboard:



To view or copy your personal access token, open the [official portal page](<https://developer.webex.com/docs/getting-your-personal-access-token>) and sign in.



<br/>

You can also obtain your personal access token from the Try It section of any API reference page.

![Try it personal access token](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt940cd395b3fb39a0/62ec0d867e18987096ab9ea8/try-it-personal-access-token.png)

## Use your personal access token

You use your personal access token like any API access token, for example:

```bash
$ curl --request GET \
  --header "Authorization: Bearer <YOUR_PERSON_ACCESS_TOKEN>" \
  https://webexapis.com/v1/rooms/
```

## Next steps

Personal access tokens are for testing with your own account. When your application is ready to access Webex on behalf of other users, [create a Webex Integration](https://developer.webex.com/docs/integrations), review the available [Integration Scopes](https://developer.webex.com/docs/integration-scopes), and implement the [OAuth authentication flow](https://developer.webex.com/docs/authentication).
