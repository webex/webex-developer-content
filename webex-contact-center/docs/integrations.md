---
type: Guide
title: Integrations & Authorization
display_title: Integrations
canonical_url: https://developer.webex.com/docs/integrations
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

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/integrations)

Create a Webex integration when your application needs a user to authorize access to Webex APIs on their behalf.

[Create an Integration](<https://developer.webex.com/my-apps/new/integration>)

## When to use an integration

An integration is an OAuth 2.0 client registered with Webex. It receives a temporary access token after a Webex user signs in and approves the requested scopes. Use an integration for applications that act on behalf of a user and can send that user through an interactive authorization flow.

You don't need to register an integration to explore the APIs with your own [personal access token](https://developer.webex.com/docs/getting-your-personal-access-token).

For unattended, organization-wide automation that should not depend on a user's lifecycle, use a Service App. Webex Contact Center developers should see [Contact Center Service Apps](https://developer.webex.com/webex-contact-center/docs/contact-center-service-apps).



## Create an integration

1. Sign in and open [My Webex Apps](https://developer.webex.com/my-apps).
2. Select **Create a New App**, then select **Create an Integration**.
3. Enter a user-facing name and description, and add an icon.
4. Add each redirect URI that your application can use for the OAuth callback.
5. Select only the [integration scopes](https://developer.webex.com/docs/integration-scopes) required by your application.
6. Save the integration and copy its client ID and client secret.

The client secret is shown only when the integration is created. Store it securely and never expose it in browser or mobile application code.



> **Info**
>
> Each Webex user account is limited to 20 integrations.



## Webex Contact Center requirements

Webex Contact Center integrations use the same registration and OAuth flow as other Webex integrations. The user who authorizes the integration must have the permissions required by the APIs that it calls.

For administrator APIs, use a Webex account backed by Cisco Webex Common Identity and assign the appropriate Webex Contact Center administrator role in Control Hub. See [Webex Contact Center administrator roles and privileges](https://help.webex.com/en-us/article/n5jdj19/Webex-Contact-Center-administrator-roles-and-privileges).

## Scopes

Scopes control which resources and operations the integration can access. Review [Integration Scopes](https://developer.webex.com/docs/integration-scopes), select the minimum required access during registration, and request the same registered scopes during authorization.





## Authorize your integration

After registration, implement the [Authentication](https://developer.webex.com/docs/authentication) flow to request user authorization, handle the callback, exchange the authorization code, refresh access, and call Webex APIs.
