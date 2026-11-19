---
type: Guide
title: Create Your Own GitHub Enterprise Bot Integrated with Webex | Consolidated Guide
display_title: Create Your Own GitHub Enterprise Bot Integrated with Webex
canonical_url: https://developer.webex.com/docs/create-your-own-github-enterprise-bot-integrated-with-webex
content_type: documentation
product_group:
- webex-suite
categories:
- create
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/create-your-own-github-enterprise-bot-integrated-with-webex)

This article explains how you can create your own Webex-integrated GitHub Enterprise bot.

## Prerequisites

Before continuing, you will need access to a few developer resources and the Node.js framework:

- **GitHub Account**:  You'll need GitHub account: [https://github.com/signup](https://github.com/signup).
- **Cisco Webex Account**: You'll need a Webex developer account if you don't have one already. You can create one on the Webex Developer Portal: [https://developer.webex.com/](https://developer.webex.com/).
- **Node.js**: To create the Webex bot, you'll be leveraging the Webex Node Bot framework. Make sure you've got [Node.js](https://nodejs.org/en/download) installed on your platform of choice.

## Build the Bot

Once you have your accounts set up and Node.js installed, follow these steps to create your own GitHub bot:

1. Login into your GitHub administrator account.
1. Select the **Settings** menu and then select **Webhooks** in the left panel.
1. Select the **Add webhook** button.
1. Configure the webhook by pasting the webhook URL you've created for the bot and select **Finish**.
    Your bot listens to this webhook for triggered events.
1. Set the **Content type** to `application/json`.
1. Enter additional information as needed in the other fields, make sure **Active** is enabled, and select **Add webhook**.
1. Log in to [Webex for Developers](https://developer.webex.com/).
1. Create your Webex bot at: [https://developer.webex.com/my-apps/new/bot](https://developer.webex.com/my-apps/new/bot).
1. Note down the bot's access token, which you'll use to make API requests.

## Use the Webex Node Bot Framework

To simplify the creation of your bot, you can use the Webex Node Bot Framework available on GitHub. This framework provides a robust and easy to use platform for handling bot interactions:

- [https://github.com/webex/webex-node-bot-framework](https://github.com/webex/webex-node-bot-framework)

For any queries related to bot framework you can join the following Webex space: [Webex-Node-Bot-Framework Support](https://eurl.io/#BJ7gmlSeU).

## Additional Resources

For more information on GitHub and Webex, see:

- **GitHub API Documentation**: [https://docs.github.com/en/rest/quickstart](https://docs.github.com/en/rest/quickstart)
- **Webex API Documentation**: [https://developer.webex.com/docs](https://developer.webex.com/docs)
