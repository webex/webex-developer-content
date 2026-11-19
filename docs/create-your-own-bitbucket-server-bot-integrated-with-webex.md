---
type: Guide
title: Create Your Own Bitbucket Server Bot Integrated with Webex | Consolidated Guide
display_title: Create Your Own Bitbucket Server Bot Integrated with Webex
canonical_url: https://developer.webex.com/docs/create-your-own-bitbucket-server-bot-integrated-with-webex
content_type: documentation
product_group:
- webex-suite
categories:
- create
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/create-your-own-bitbucket-server-bot-integrated-with-webex)

This article explains how you can create your own Webex-integrated Bitbucket Server bot.

## Prerequisites

To get started with your Bitbucket Server bot, you will need access to a few developer resources:

- **Bitbucket Account**: You'll need to apply for an account in: [https://id.atlassian.com/signup](https://id.atlassian.com/signup).
- **Cisco Webex Account**: You'll need a Webex developer account if you don’t have one already. You can create one on the Webex Developer Portal: [https://developer.webex.com/](https://developer.webex.com/).
- **Node.js**: To create the Webex bot, you’ll be leveraging the Webex Node Bot framework. Make sure you’ve got [Node.js](https://nodejs.org/en/download) installed on your platform of choice.

## Build the Bot

Once you have your accounts set up and Node.js installed, follow these steps to create your own Bitbucket Server bot:

1. Log in to your Bitbucket account as and administrator.
1. Select the drop-down arrow next to the **Repositories** menu and select the repository for which you want to create a webhook.
1. Choose **Webhooks** in the left-side panel and then select **Create webhook**.
1. Enter the following information:
    - **Name**: Enter a name for the webhook.
    - **URL**: Paste the webhook URL that you’ve created for the bot and select **Finish**. Your bot listens to this webhook for triggered events.
    - **Events**: Select all **Repository** and **Pull request** events.
    - **Active**: Make sure **Active** is enabled.
1. Select **Create**.
1. Log in to [Webex for Developers](https://developer.webex.com/).
1. Create your Webex bot at: [https://developer.webex.com/my-apps/new/bot](https://developer.webex.com/my-apps/new/bot).
1. Note down the bot's access token, which you'll use to make API requests.

## Use the Webex Node Bot Framework

To simplify the creation of your bot, you can use the Webex Node Bot Framework available on GitHub. This framework provides a robust and easy to use platform for handling bot interactions:

- [https://github.com/webex/webex-node-bot-framework](https://github.com/webex/webex-node-bot-framework)

For any queries related to bot framework you can join the following Webex space: [Webex-Node-Bot-Framework Support](https://eurl.io/#BJ7gmlSeU).

## Additional Resources

For more information on Bitbucket Server and Webex, see:

- **Bitbucket API Documentation**: [https://developers.wrike.com/overview/](https://developers.wrike.com/overview/)
- **Webex API Documentation**: [https://developer.webex.com/docs](https://developer.webex.com/docs)
