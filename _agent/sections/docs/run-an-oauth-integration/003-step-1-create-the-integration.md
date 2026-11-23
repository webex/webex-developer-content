---
type: Excerpt
canonical_url: https://developer.webex.com/docs/run-an-oauth-integration
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- 'Step 1: Create the Integration'
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/run-an-oauth-integration). [Full Markdown](../../../../docs/run-an-oauth-integration.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites](002-prerequisites.md)

## Article introduction

This tutorial shows you how to get a Node.js server running locally that acts as an OAuth client for a Webex [integration](https://developer.webex.com/docs/integrations), obtain an API access token for the authenticating user, and uses it to call a Webex API to get information about the user.

## Selected section

## Step 1: Create the Integration

First you'll create a Webex [Integration](https://developer.webex.com/docs/integrations), which represents an OAuth client. An OAuth client ID and secret is generated that you'll use to configure the Node.js app. You also specify the redirect URL where the user is sent after they authenticate with Webex and accept the requested data access scopes. In this case the redirect URL is set to **http://localhost:8080** where the Node.js server will be listening for requests from the Webex OAuth server.

**To create the Webex integration**:

1. Open the [New Integration](https://developer.webex.com/my-apps/new/integration) page on the Developer Portal (you must be [signed in](https://developer.webex.com/login)).

2. Enter a name and description and select (or upload) an app icon.

    The integration's name and icon are displayed on the OAuth consent page where the authenticated user accepts (or denies) your app's request for the requested data scopes. The description is only used if or when you publish your integration to Webex [AppHub](https://apphub.webex.com).

3. For **Redirect URL** enter **http://localhost:8080/oauth**.

    ![Redirect URI](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt77ab3c56e98cf675/636060b47a7bad106b9ae831/redirect_uri.png)

    This is where the local Node.js app will be listening for requests.

4. In the **Scopes** section select the **spark:people_read** scope.

    ![Scopes](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte51fc07ff661f8a6/6360619757082b10e8175cb8/add-scopes.png)

5. Click **Add Integration**.

6. Copy the your integration's generated **Client ID** and **Client Secret** for use in the next step.

    ![Client ID and secret](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt2135a5986a9d0ebd/636068df882b96108ae799bc/client_id_secret_copy.png)

7. Copy the **OAuth Authorization URL** string for use in the next step.

    ![OAuth authorization URL](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt8e73870d76ee936b/6373e69371c75510a0c9e16d/auth-init-url-2.png)

    This string contains URL-encoded values for the integration's requested scopes, client ID, redirect URL and state. The Node.js app will compute a new `state` query parameter value and add it to the URL.

    

> **Info**
>
> You could instead compose this URL in code, but typically the URL won't change much once your integration. This way you can't accidentally forget about including a selected scope.
