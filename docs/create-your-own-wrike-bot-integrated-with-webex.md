---
type: Guide
title: Create Your Own Wrike Bot Integrated with Webex | Consolidated Guide
display_title: Create Your Own Wrike Bot Integrated with Webex
canonical_url: https://developer.webex.com/docs/create-your-own-wrike-bot-integrated-with-webex
content_type: documentation
product_group:
- webex-suite
categories:
- create
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/create-your-own-wrike-bot-integrated-with-webex)

This article explains how you can create your own Webex-integrated Wrike bot.

## Prerequisites

Before continuing, you will need access to a few developer resources and the Node.js framework:

- **Wrike Account**:  You'll need to apply for an account in: [https://www.wrike.com/](https://www.wrike.com/).
- **Cisco Webex Account**: You'll need a Webex developer account if you don't have one already. You can create one on the Webex Developer Portal: [https://developer.webex.com/](https://developer.webex.com/).
- **Node.js**: To create the Webex bot, you'll be leveraging the Webex Node Bot framework. Make sure you've got [Node.js](https://nodejs.org/en/download) installed on your platform of choice.

## Build the Bot

Once you have your accounts set up and Node.js installed, follow these steps to create your own Wrike bot:

1. Once logged in to Wrike, navigate to the **Apps and Integrations** section.
1. Inside **Apps and Integrations**, go to the **API** tab.
1. Click on **Create new**.
1. You'll be asked to provide some basic details for your app. This includes:
    - **App Name**: The name of your application.
    - **App Description**: A short description of your app.
    - **Redirect URI(s)**: This is critical. The user is directed to this URI after authorizing within your app. You must specify it upfront, as part of the OAuth flow.
1. A Client ID and Client secret are created. Make sure you make a note of them.
1. Log in to [Webex for Developers](https://developer.webex.com/).
1. Create your Webex bot at: [https://developer.webex.com/my-apps/new/bot](https://developer.webex.com/my-apps/new/bot).
1. Note down the bot's access token, which you'll use to make API requests.

## Use the Webex Node Bot Framework

To simplify the creation of your bot, you can use the Webex Node Bot Framework available on GitHub. This framework provides a robust and easy to use platform for handling bot interactions:

- [https://github.com/webex/webex-node-bot-framework](https://github.com/webex/webex-node-bot-framework)

For any queries related to bot framework you can join the following Webex space: [Webex-Node-Bot-Framework Support](https://eurl.io/#BJ7gmlSeU).

## Additional Resources

For more information on Wrike and Webex, see:

- **Wrike API Documentation**: [https://developers.wrike.com/overview/](https://developers.wrike.com/overview/)
- **Webex API Documentation**: [https://developer.webex.com/docs](https://developer.webex.com/docs)
