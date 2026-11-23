---
type: Excerpt
canonical_url: https://developer.webex.com/docs/run-an-oauth-integration
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- 'Step 3: Test the Integration'
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/run-an-oauth-integration). [Full Markdown](../../../../docs/run-an-oauth-integration.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites](002-prerequisites.md)

## Article introduction

This tutorial shows you how to get a Node.js server running locally that acts as an OAuth client for a Webex [integration](https://developer.webex.com/docs/integrations), obtain an API access token for the authenticating user, and uses it to call a Webex API to get information about the user.

## Selected section

## Step 3: Test the Integration

Next you'll test the integration by initiating the OAuth flow from your browser, signing in to your Webex account and accepting the requested data scopes on the consent screen.

**To test the integration**:

1. Open <http://localhost:8080> and click **Start OAuth Flow**.

    ![Start flow](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt9bbbd652b670c9fd/637681c6d4802c10f7f4ca6b/homepage.png)

2. Sign in to your Webex account, if prompted, and click **Accept** on the consent page.

    ![Consent screen](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt36a4934b91dd73dd/637682ba0c4e351095246a53/scope-01.png)

    Your browser is redirected to the integration's redirect URI, where the Node.js app [exchanges the authorization code](https://github.com/WebexSamples/webex-oauth-integration/blob/main/server.js#L170-L189) returned by Webex for an API access token, and [stores the token as a session variable](https://github.com/WebexSamples/webex-oauth-integration/blob/main/server.js#L170-L189). The server then uses the access token to call the [Get My Own Details](https://developer.webex.com/docs/api/v1/people/get-my-own-details) endpoint, which returns details about the authenticated user. The server [parses out the user's display name](https://github.com/WebexSamples/webex-oauth-integration/blob/main/server.js#L258-L263) from the response and returns it in a compiled EJS template.

    ![Authenticated](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt809fe25c401f5f14/637684b1acdace107758f42a/authenticated-new.png)
