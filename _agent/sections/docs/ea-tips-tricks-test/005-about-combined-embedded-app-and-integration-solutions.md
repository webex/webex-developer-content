---
type: Excerpt
canonical_url: https://developer.webex.com/docs/ea-tips-tricks-test
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- About Combined Embedded App and Integration Solutions
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/ea-tips-tricks-test). [Full Markdown](../../../../docs/ea-tips-tricks-test.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

---

**[Embedded Apps Guide](https://developer.webex.com/docs/ea-developer-guide-test) > Workflow**
* * * 

## Selected section

## About Combined Embedded App and Integration Solutions

Embedded apps can't make [Webex API](https://developer.webex.com/docs/getting-started) calls directly. However, your embedded app can be backed by a server process that acts as a [Webex Integration](https://developer.webex.com/docs/integrations). In this scenario, the embedded app prompts the user to [initiate the OAuth authorization](https://developer.webex.com/docs/integrations#requesting-permission) process to obtain an access token to make Webex API calls on the user's behalf.

First, the user clicks a button or link in the embedded app that opens the Webex authorization request URL(`https://webexapis.com/v1/authorize`). This URL is configured with your Webex integration's [requested scopes](https://developer.webex.com/docs/integrations#scopes), client ID, and redirect URL, and other [request parameters](https://developer.webex.com/docs/integrations#requesting-permission).

![Button to start OAuth flow](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt1b0e8e3193410d16/61d8813f9efff26ae759800e/oauth-flow-start.png)

Once the user has signed in to their Webex account they are asked if they want to accept the request for access to data in the specified scopes.

![Webex login screen](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltc44413802cdf4f16/61d88843bf9cb8387cc1d960/oauth-flow-login.png)

![User authorizes access to data](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltf4cd7db442aeafe7/61d8c28fdbd06039fdcf7ad5/oauth-flow-accept.png)

Once the user accepts the request they are redirected to your integration's specified **Redirect URL**, which is passed an authorization code from the authorization server. This page can [exchange the auth code](https://developer.webex.com/docs/integrations#getting-an-access-token) for an API access token to make Webex API calls (to the [/v1/people/me](https://developer.webex.com/docs/api/v1/people/get-my-own-details) API endpoint, for example) on the user's behalf and display the results in the embedded app, as shown below.

![Redirect page showing results of authenticated API call](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltbaea62e45e1e6a40/61d8c29c8b16776549dee779/oauth-flow-authenticated.png)

<a id="clear-cache"></a>
