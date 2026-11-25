---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-calling-sdk-authorization-device-registration
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Obtain an Access Token
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-calling-sdk-authorization-device-registration). [Full Markdown](../../../../../docs/sdks/webex-calling-sdk-authorization-device-registration.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Authorization and device creation are crucial initial steps in leveraging the full capabilities of the calling SDK. Authorization ensures secure access and permissions for developers, while device creation establishes the necessary endpoint for enabling voice and video communication features in your application.

## Selected section

## Obtain an Access Token

Developers can obtain an access token by leveraging Common Identity, which employs the OAuth 2.0 authorization framework for secure and standardized token-based authentication. To get up and running with the OAuth 2.0 flow, you can refer [to this detailed guide](https://developer.webex.com/docs/login-with-webex) which runs through the necessary steps, including user consent and redirection, to generate a short-lived authorization code.

After receiving the authorization code, you can use the `curl` utility with the following example API call to exchange it for an access token:

```bash
curl -X POST https://webexapis.com/v1/access_token \
  -d "grant_type=authorization_code" \
  -d "client_id=YOUR_CLIENT_ID" \
  -d "client_secret=YOUR_CLIENT_SECRET" \
  -d "code=AUTHORIZATION_CODE" \
  -d "redirect_uri=YOUR_REDIRECT_URI"
```

Once you obtain the access token, it acts as the credential for secure API interactions with various Webex services, including the `CallingClient` module. The developer.webex.com website serves as a comprehensive resource throughout this OAuth 2.0 process, enabling you to seamlessly integrate Webex features into your application while mitigating security concerns.



> **Info**
>
> To authorize with Webex Calling, a developer must select the appropriate scopes while creating the Integration, or pass these scopes if directly creating an access token. [Scopes](https://developer.webex.com/docs/integrations#scopes) define the level of access that an integration requires. Webex Calling requires these scopes: `spark:webrtc_calling`, `spark:calls_read`, `spark:calls_write`, and `spark:xsi`.
