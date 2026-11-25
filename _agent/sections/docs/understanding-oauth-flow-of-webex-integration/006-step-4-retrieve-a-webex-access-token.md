---
type: Excerpt
canonical_url: https://developer.webex.com/docs/understanding-oauth-flow-of-webex-integration
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- 'Step 4: Retrieve a Webex access token'
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/understanding-oauth-flow-of-webex-integration). [Full Markdown](../../../../docs/understanding-oauth-flow-of-webex-integration.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Step 2: Registering a custom Webex integration](004-step-2-registering-a-custom-webex-integration.md)

## Article introduction

This tutorial demonstrates how to perform Webex OAuth2 authentication for a Webex Integration.

## Selected section

## Step 4: Retrieve a Webex access token

We should now be ready to try out the sample app using your new **Webex** application registration info to log in and generate an access token:

1. Make sure the following are ready:

    - **Webex** user account email and password
    - Application **Client ID**
    - Application **Client Secret**
    - Application **Redirect URI**
    - The authentication [sample app](https://developer.cisco.com/learning/posts/files/collab-spark-auth/webex-teams-auth.html) is open

2. Using the sample app, login and request the **Webex** auth code:

    - Copy and paste the application **Client ID**, into the appropriate field (Client Secret is not needed in this step).
    - Click **Request Auth Code**, then follow the directions shown in the sample app to view/confirm the requested application permissions, and log in.  When finished, the sample app page should reload and populate the 'Auth Code' field.

3. Exchange the auth code for the **Webex** API access token:

    - Copy and paste the application **Client ID** (once again), and **Client Secret** into the appropriate fields.
    - Click **Request Access Token**.

The access token should be displayed in the 'Access Token' box.  



> **Info**
>
> While not displayed in this sample app, some additional info - such as token expiration info and a refresh token, is also included in the response.



For example:

```json
{
  "access_token": "XXXXX"
  "expires_in": 1209599
  "refresh_token": "YYYY"
  "refresh_token_expires_in": 7775082
}
```

This info shows that the **Webex** API access token expires in just under 14 days (1209599 seconds.)  After that time, the application can use the `refresh_token` to obtain a new access token.  The refresh token itself is good for about 90 days, renewed whenever it is used to retrieve an access token.



> **Info**
>
> See the [Integrations and OAuth](https://developer.webex.com/docs/integrations) page for more details on refresh tokens.
