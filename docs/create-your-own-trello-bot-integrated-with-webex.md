---
type: Guide
title: Create Your Own Trello Bot Integrated with Webex | Consolidated Guide
display_title: Create Your Own Trello Bot Integrated with Webex
canonical_url: https://developer.webex.com/docs/create-your-own-trello-bot-integrated-with-webex
content_type: documentation
product_group:
- webex-suite
categories:
- create
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/create-your-own-trello-bot-integrated-with-webex)

Follow the instructions in this article to create your own Trello bot for Webex.

## Prerequisites

To get started with your Trello bot, you will need access to a few developer resources:

- **Trello Account**:  You'll need Trello account: [https://trello.com/](https://trello.com/)
- **Cisco Webex Account**: You'll need a Webex developer account if you don't have one already. You can create one on the Webex Developer Portal: [https://developer.webex.com/](https://developer.webex.com/)
- **Node.js**: To create the Webex bot, you'll be leveraging the Webex Node Bot framework. Make sure you've got [Node.js](https://nodejs.org/en/download) installed on your platform of choice.

## Build the Bot

Once you have your accounts set up and Node.js installed, follow these steps to create your own Trello bot

1. Login to the [Power-Up Admin Portal](https://trello.com/power-ups/admin/), select **New** and enter the following details:
    - **Power-up name**: Enter a name for your power-up.
    - **Select Workspace**: Choose a workspace.
    - **Iframe connector URL**: Enter a URL HTML that Trello loads as a hidden iframe and uses to communicate with your power-up.
    - **Email**: Enter an support email address.
    - **Support contact**: Enter the name for the power-up support contact.
    - **Author**: Enter the author of the power-up.
1. Select **Create**.
1. On the API key page, select **Generate** to generate a new API key and make note of the following information:
    - **API key**: Keep your API Secret safe. Since your API Key is public for any client-side applications, there is no way to reset it.
    - **Allowed Origins**: Specify the origins (e.g. https://example.com) that your application is allowed to redirect back to following the authorization flow. Trello prevents redirects to any origin not specified here.
    - **Secret**: If you want to use OAuth 1 authorization, you'll need this secret.
1. Log in to [Webex for Developers](https://developer.webex.com/).
1. Create your Webex bot at: [https://developer.webex.com/my-apps/new/bot](https://developer.webex.com/my-apps/new/bot).
1. Note down the Bot's Access Token, which you'll use to make API requests.

## Use the Webex Node Bot Framework

To simplify the creation of your bot, you can use the Webex Node Bot Framework available on GitHub. This framework provides a robust and easy to use platform for handling bot interactions:

- [https://github.com/webex/webex-node-bot-framework](https://github.com/webex/webex-node-bot-framework)

For any queries related to bot framework you can join the following Webex space: [Webex-Node-Bot-Framework Support](https://eurl.io/#BJ7gmlSeU).

## Additional Resources

For more information on Trello and Webex, see:

- **Trello Documentation**: [https://developer.atlassian.com/cloud/trello/](https://developer.atlassian.com/cloud/trello/).
- **Webex API Documentation**: [https://developer.webex.com/docs](https://developer.webex.com/docs).
