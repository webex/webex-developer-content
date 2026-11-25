---
type: Excerpt
canonical_url: https://developer.webex.com/docs/run-an-oauth-integration
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- 'Step 4: List the User''s Spaces'
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/run-an-oauth-integration). [Full Markdown](../../../../docs/run-an-oauth-integration.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites](002-prerequisites.md)

## Article introduction

This tutorial shows you how to get a Node.js server running locally that acts as an OAuth client for a Webex [integration](https://developer.webex.com/docs/integrations), obtain an API access token for the authenticating user, and uses it to call a Webex API to get information about the user.

## Selected section

## Step 4: List the User's Spaces

Next you'll add a new scope to your integration that will allow your app to get a list of Webex spaces (called "rooms" in the API) the user has recently visited, and modify the Node app to let the user view a list of their spaces.

**To list the user's spaces**:

1. Update your [Webex integration](https://developer.webex.com/my-apps) to include the **spark:rooms_read** data scope. 

2. Save your changes to the integration and copy the new authorization URI paste it into  the project's **.env** file for the `AUTH_INIT_URL` variable, as before. This URL contains the newly added scope.

3. In the Node project uncomment the following line in [www/display-name.ejs](https://github.com/WebexSamples/webex-oauth-integration/blob/main/www/display-name.ejs#L17). An [Express route](https://github.com/WebexSamples/webex-oauth-integration/blob/main/server.js#L215) for this path is pre-defined in server.js.

    ```html
    <a href="/listrooms">List my rooms (spaces)</a>
    ```

4. Restart the Node.js application and repeat the login and consent process. Note that the consent screen asks for an additional scope ("List titles of spaces that you are in").

    ![New scope consent screen](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltcd6374456545a34a/63766fb776567a10a7cb8427/accept-new-scope.png)

5. On the greeting page click **List my Rooms** to display a list of your recently visited rooms.

    ![List of rooms](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltf0713a92b8e6db49/63768f1e32130110b2799817/list-rooms.png)
