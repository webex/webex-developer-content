---
type: Excerpt
canonical_url: https://developer.webex.com/docs/understanding-oauth-flow-of-webex-integration
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- 'Step 2: Registering a custom Webex integration'
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/understanding-oauth-flow-of-webex-integration). [Full Markdown](../../../../docs/understanding-oauth-flow-of-webex-integration.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This tutorial demonstrates how to perform Webex OAuth2 authentication for a Webex Integration.

## Selected section

## Step 2: Registering a custom Webex integration

**Webex** developers can define new integrated applications by logging into the Webex [Developer Portal](https://developer.webex.com/docs/integrations) and providing a couple of details.  Creating an app registration accomplishes a few things:

- Generates a unique application **Client ID** and **Client Secret**, needed to access the Webex authentication service
- Identifies the application's defined **scopes** (**Webex** service permissions)
- Specifies a **Redirect URI** for the application, where **Webex** OAuth2 authentication responses will be sent



> **Info**
>
> For more details on **Webex** OAuth2 authentication, see [Developer Portal - Apps & OAuth](https://developer.webex.com/docs/integrations)



1. Determine the app's **Redirect URI**.  The **Webex** OAuth2 flow will redirect the user's browser to a number of different sites and URLs during the authentication sequence.  When complete, **Webex** will need a way to send the browser back to the custom web app (with the OAuth2 authentication code attached.)  This is done by specifying a unique **Redirect URL** URL which points back to the web application.  In our case, the URL for the web page itself will be re-used as the **Redirect URI**:

    - Open the [sample app](https://developer.cisco.com/learning/posts/files/collab-spark-auth/webex-teams-auth.html) in a new tab
    - Copy the **Redirect URI** field value to the clipboard (the sample app detects this URL automatically)
    ![URL Screen Shot](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltd12f77dccc5416ce/61f00cf6904d9713809835fb/url_from_sample.png)

2. Navigate to the **Developer Portal** application registration page:

    - Open a new browser tab, and navigate to the [Developer Portal]() page.
    - If you like, click **Go to Docs** and take a tour of the **Webex** API docs.
    - Log in.
    - Once logged in, click on your avatar and select [My Webex Apps](https://developer.webex.com/my-apps)
    ![My Webex Apps](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt3c360ba775a546b9/61f023d4a96c4414ac4342cd/my_webex_apps.png).
    - In the **Create a new App** page, click **Create an Integration**.

3. Complete the **New Integration** form with the following details, and then click **Add Integration**:

    - **Integration Name** - Enter any application name you like (e.g., 'test app').
    - **Icon** - Upload an icon image or choose one of the defaults (note the size requirements).
    - **Description** - Enter any description you like.
    - **Redirect URI(s)s** - Paste or enter the **Redirect URI** that was displayed in the sample app (see above).
    - **Scopes** - Check the scope: `spark:rooms_read`.

4. Check the confirmation message, and note your application's generated **Client ID**, **Client Secret**, and the **OAuth Authorization URL**. You will use these later to perform the **Webex** authentication request.  You can use this [note-box page](https://developer.cisco.com/learning/posts/files/collab-webex-auth/notebox.html) to copy/paste into temporarily.
![Screen Shot](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt4ab6929c824130fa/61f00ce7e30aaf137e48ca68/secrets.png)



> **Info**
>
> Note: For production apps, record your **Client ID** and **Client Secret** in a safe place.  The **Client Secret** will not be displayed again (though you can generate a new one).
