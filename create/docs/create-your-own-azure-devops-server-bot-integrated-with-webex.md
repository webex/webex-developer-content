---
type: Guide
title: Create Your Own Azure DevOps Server Bot Integrated with Webex | Consolidated Guide
display_title: Create Your Own Azure DevOps Server Bot Integrated with Webex
canonical_url: https://developer.webex.com/docs/create-your-own-azure-devops-server-bot-integrated-with-webex
content_type: documentation
product_group:
- webex-suite
categories:
- create
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/create-your-own-azure-devops-server-bot-integrated-with-webex)

This article explains how you can create your own Webex-integrated Azure DevOps Server bot.

## Prerequisites

Before continuing, you will need access to a few developer resources and the Node.js framework:

- **Developer Account**:&#xa0;You'll need Azure DevOps Server account: [https://azure.microsoft.com/en-us/pricing/purchase-options/azure-account](https://azure.microsoft.com/en-us/pricing/purchase-options/azure-account). You must be a project administrator for your Azure DevOps Server account.
- **Cisco Webex Account**:&#xa0;You'll need a Webex developer account if you don't have one already. You can create one on the Webex Developer Portal:&#xa0;[https://developer.webex.com/](https://developer.webex.com/).
- **Node.js**: To create the Webex bot, you'll be leveraging the Webex Node Bot framework. Make sure you've got [Node.js](https://nodejs.org/en/download) installed on your platform of choice.

## Build the Bot

Once you have your accounts set up and Node.js installed, follow these steps to create your own Azure DevOps Server bot:

1. Login to the [Azure DevOps Server Portal](https://azure.microsoft.com/en-us/get-started/azure-portal) and select **Projects**.
1. Select the project you'd like to use for your Webex bot.
1. Select the **Settings** icon and choose **Service Hooks**.
1. Select **Create subscription**.
1. Select **Web Hooks** in the left panel and choose **Next**.
1. In **Trigger** configuration, select the trigger event for which you would like to set up a webhook and choose **Next**.
1. In the **Action** configuration, paste the webhook URL that you've created for the bot and select **Finish**.
    Your bot listens to this webhook for triggered events.
1. Log in to [Webex for Developers](https://developer.webex.com/).
1. Create your Webex bot at: [https://developer.webex.com/my-apps/new/bot](https://developer.webex.com/my-apps/new/bot).
1. Note down the bot's access token, which you'll use to make API requests.

## Use the Webex Node Bot Framework

To simplify the creation of your bot, you can use the Webex Node Bot Framework available on GitHub. This framework provides a robust and easy to use platform for handling bot interactions:

- [https://github.com/webex/webex-node-bot-framework](https://github.com/webex/webex-node-bot-framework)

For any queries related to bot framework you can join the following Webex space: [Webex-Node-Bot-Framework Support](https://eurl.io/#BJ7gmlSeU).

## Additional Resources

For more information on Azure DevOps Server and Webex, see:

- **Azure DevOps Server**: [https://developers.wrike.com/overview/](https://developers.wrike.com/overview/)
- **Webex API Documentation**: [https://developer.webex.com/docs](https://developer.webex.com/docs)
