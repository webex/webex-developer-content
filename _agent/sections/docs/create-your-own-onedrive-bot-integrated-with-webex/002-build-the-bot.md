---
type: Excerpt
canonical_url: https://developer.webex.com/docs/create-your-own-onedrive-bot-integrated-with-webex
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Build the Bot
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/create-your-own-onedrive-bot-integrated-with-webex). [Full Markdown](../../../../docs/create-your-own-onedrive-bot-integrated-with-webex.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites](001-prerequisites.md)

## Article introduction

This article explains how you can create your own Webex-integrated OneDrive bot.

## Selected section

## Build the Bot

Once you have your accounts set up and Node.js installed, follow these steps to create your own OneDrive bot:

1. Sign into the [Azure portal](https://portal.azure.com/) with your Microsoft account that has Azure Active Directory privileges.
1. In the Azure portal, search for and select **Azure Active Directory.**
1. In the left pane, under **Manage**, select **App registrations**.
1. Select **New registration** at the top of the page.
1. Fill in the following registration details:
    - **Name**: Choose a name for your application (for example, `OneDrive OAuth App`).
    - **Supported account types**: Select the accounts you require from any organizational directory or personal Microsoft accounts (This will allow you to access OneDrive data across all types of users).
    - **Redirect URI**: Select **Web** and provide a URI where you will receive the authorization code after login.
1. Select **Register** to create the app.
1. Navigate to the app's **API permissions** section in the Azure portal.
1. Select **Add a permission** and then select **Microsoft Graph**.
1. Search for and add the following scopes: `files.read`, `offline_access`.
1. In **Certificates &amp; secrets**, select **New client secret**:
1. Add a description and set an expiration for the secret.
1. Copy the client secret and save it securely, (you can’t retrieve it later).
1. In the **Overview** section, copy the **Application (client) ID** and **Directory (tenant) ID**.
1. Implement the OAuth Flow in Your App:
    1. Retrieve an authorization code from the user:
        Use the app you created above to authenticate the user. You will be redirected to a login/authorization page (hosted by Microsoft) and prompted to sign in and consent to the permissions your app needs. Once permission is granted, Microsoft will direct back to your app with an **authorization code.**
    1. **Exchange the authorization code for an access token:**
        Your app sends this authorization code to Microsoft’s server in exchange for an **access token and refresh token.** The access token is what your app uses to authenticate API requests.
    1. **Use the token to interact with the Microsoft Graph API:**
        Now that your app has the access token, it can use it to make authorized requests to the **Microsoft Graph API**, which allows you to access data from Microsoft services on behalf of the user.
1. Log in to [Webex for Developers](https://developer.webex.com/).
1. Create your Webex bot at: [https://developer.webex.com/my-apps/new/bot](https://developer.webex.com/my-apps/new/bot).
1. Note down the bot's access token, which you'll use to make API requests.
