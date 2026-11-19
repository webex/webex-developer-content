---
type: Guide
title: Create Your Own OneDrive Bot Integrated with Webex | Consolidated Guide
display_title: Create Your Own OneDrive Bot Integrated with Webex
canonical_url: https://developer.webex.com/docs/create-your-own-onedrive-bot-integrated-with-webex
content_type: documentation
product_group:
- webex-suite
categories:
- create
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/create-your-own-onedrive-bot-integrated-with-webex)

This article explains how you can create your own Webex-integrated OneDrive bot.

## Prerequisites

Before continuing, you will need access to a few developer resources and the Node.js framework:

- **Microsoft Developer Account**: You'll need to apply for a developer account to get access to the APIs available on the Microsoft Portal: [https://signup.live.com/](https://signup.live.com/).
- **Cisco Webex Account**:&#xa0;You'll need a Webex developer account if you don’t have one already. You can create one on the Webex Developer Portal:&#xa0;[https://developer.webex.com/](https://developer.webex.com/).
- **Node.js**: To create the Webex bot, you’ll be leveraging the Webex Node Bot framework. Make sure you’ve got [Node.js](https://nodejs.org/en/download) installed on your platform of choice.

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

## Use the Webex Node Bot Framework

To simplify the creation of your bot, you can use the Webex Node Bot Framework available on GitHub. This framework provides a robust and easy to use platform for handling bot interactions:

- [https://github.com/webex/webex-node-bot-framework](https://github.com/webex/webex-node-bot-framework)

For any queries related to bot framework you can join the following Webex space: [Webex-Node-Bot-Framework Support](https://eurl.io/#BJ7gmlSeU).

## Additional Resources

For more information on OneDrive and Webex, see:

- **OneDrive API Documentation**: [https://learn.microsoft.com/en-us/graph/api/resources/onedrive?view=graph-rest-1.0](https://learn.microsoft.com/en-us/graph/api/resources/onedrive?view=graph-rest-1.0).
- **Webex API Documentation**: [https://developer.webex.com/docs](https://developer.webex.com/docs).
