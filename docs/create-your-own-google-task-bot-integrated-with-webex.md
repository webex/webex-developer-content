---
type: Guide
title: Create Your Own Google Task Bot Integrated with Webex | Consolidated Guide
display_title: Create Your Own Google Task Bot Integrated with Webex
canonical_url: https://developer.webex.com/docs/create-your-own-google-task-bot-integrated-with-webex
content_type: documentation
product_group:
- webex-suite
categories:
- create
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/create-your-own-google-task-bot-integrated-with-webex)

This article explains how you can create your own Webex-integrated Google Task bot.

## Prerequisites

Before continuing, you will need access to a few developer resources and the Node.js framework:

- **Google Developer Account**: You'll need to apply for a developer account on the Google Cloud Platform to access the Google Task APIs. You can apply for one at the Google Cloud Console: [Webex for Developers](https://console.cloud.google.com/).
- **Cisco Webex Account**: You'll need a Webex developer account if you don’t have one already. You can create one on the Webex Developer Portal: <https://developer.webex.com/>.
- **Node.js**: To create the Webex bot, you’ll be leveraging the Webex Node Bot framework. Make sure you’ve got [Node.js](https://nodejs.org/en/download) installed on your platform of choice.

## Build the Bot

Once you have your accounts set up and Node.js installed, follow these steps to create your own Google Task bot:

1. Login to the [Google Cloud Console](https://console.cloud.google.com/).
1. Create a new project or select an existing project.
1. Navigate to **APIs &amp; Services** and then **Credentials**.
1. Select **Create Credentials** and then select **OAuth Client ID**.
1. Set the application type to **Web application**.
1. Under the **Authorized redirect URIs** section, add the URI where your application will handle the OAuth 2.0 response. This is typically your server's endpoint that handles token exchanges.
    Note down the **Client ID** and **Client Secret** for future use.
1. In the Google Cloud Console, navigate to **APIs &amp; Services** and then **Library**.
1. Search for **Google Tasks API** and enable it for your project.
1. Under APIs and Services, go to OAuth 2.0 consent screen tab, ensure you include the following scope to allow your bot to view, create, and edit tasks:
    - `https://www.googleapis.com/auth/tasks` - Full access to the user's tasks.
    - `https://www.googleapis.com/auth/tasks.readonly` - View the user's tasks.
1. Log in to <https://developer.webex.com/>.
1. Create your Webex bot at: [https://developer.webex.com/my-apps/new/bot](https://developer.webex.com/my-apps/new/bot).
1. Note down the bot's access token, which you'll use to make API requests.

## Build the OAuth App

To build the app:

1. Use the Google Tasks API to authenticate users and access their tasks.
1. Use the Webex Messages API to post task updates to a Webex space.
1. When a task is created or updated in Google Tasks, use the Webex API to send a message to the relevant Webex space.

## Test and Deploy

Make sure you:

1. Test the integration thoroughly to ensure tasks are being created, viewed, and edited as expected.
1. Deploy the bot on a server and ensure it is accessible to handle requests and manage token exchanges.

## Use the Webex Node Bot Framework

To simplify the creation of your bot, you can use the Webex Node Bot Framework available on GitHub. This framework provides a robust and easy to use platform for handling bot interactions:

- [https://github.com/webex/webex-node-bot-framework](https://github.com/webex/webex-node-bot-framework)

For any queries related to bot framework you can join the following Webex space: [Webex-Node-Bot-Framework Support](https://eurl.io/#BJ7gmlSeU).

## Additional Resources

For more information on Google Tasks and Webex, see:

- **Google Tasks API Documentation**: [https://developers.google.com/tasks](https://developers.google.com/tasks).
- **Webex API Documentation**: [https://developer.webex.com/docs](https://developer.webex.com/docs).
