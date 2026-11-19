---
type: Guide
title: Create Your Own HubSpot Bot Integrated with Webex | Consolidated Guide
display_title: Create Your Own HubSpot Bot Integrated with Webex
canonical_url: https://developer.webex.com/docs/create-your-own-hubspot-bot-integrated-with-webex
content_type: documentation
product_group:
- webex-suite
categories:
- create
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/create-your-own-hubspot-bot-integrated-with-webex)

This article explains how you can create your own Webex-integrated HubSpot bot.

## Prerequisites

Before continuing, you will need access to a few developer resources and the Node.js framework:

- **HubSpot Developer Account**: You'll need to apply for a developer account to get access to the APIs available in the HubSpot: [https://developers.hubspot.com/](https://developers.hubspot.com/).
- **Cisco Webex Account**:&#xa0;You'll need a Webex developer account if you don’t have one already. You can create one on the Webex Developer Portal:&#xa0;[https://developer.webex.com/](https://developer.webex.com/).
- **Node.js**: To create the Webex bot, you’ll be leveraging the Webex Node Bot framework. Make sure you’ve got [Node.js](https://nodejs.org/en/download) installed on your platform of choice.

## Build the Bot

Once you have your accounts set up and Node.js installed, follow these steps to create your own Hubspot bot:

1. Login to your [HubSpot developer account](https://developers.hubspot.com/), and navigate to **Apps** in the top nav.
1. Select **Create app** and choose **Custom App** for the app type.
1. Enter a name for your app, for example, `Contacts API Integration`.
1. Choose OAuth as the **app type**.
1. Add your **OAuth Redirect URL**. This is where HubSpot will redirect users after they authorize the app.
1. Optionally, add a **Logo** and an **App Description** and select **Create App**.
1. Go to the **Scopes** section in the app settings and select the following scopes:
    - `content`
    - `crm.lists.read`
    - `crm.lists.write`
    - `crm.objects.companies.read`
    - `crm.objects.companies.write`
    - `crm.objects.contacts.read`
    - `crm.objects.contacts.write`
    - `crm.objects.deals.read`
    - `crm.objects.deals.write`
    - `files`
    - `forms`
    - `oauth`
    - `sales-email-read`
1. Navigate to the **Auth** section of the app settings.
    HubSpot provides you with a Client ID and Client Secret. Keep these credentials&#xa0;&#xa0; secure, as you'll need them for the OAuth flow.
1. Log in to [Webex for Developers](https://developer.webex.com/).
1. Create your Webex bot at: [https://developer.webex.com/my-apps/new/bot](https://developer.webex.com/my-apps/new/bot).
1. Note down the bot's access token, which you'll use to make API requests.

## Use the Webex Node Bot Framework

To simplify the creation of your bot, you can use the Webex Node Bot Framework available on GitHub. This framework provides a robust and easy to use platform for handling bot interactions:

- [https://github.com/webex/webex-node-bot-framework](https://github.com/webex/webex-node-bot-framework)

For any queries related to bot framework you can join the following Webex space: [Webex-Node-Bot-Framework Support](https://eurl.io/#BJ7gmlSeU).

## Additional Resources

For more information on HubSpot and Webex, see:

- **HubSpot API Documentation**: [https://developers.hubspot.com/beta-docs/reference/api/overview](https://developers.hubspot.com/beta-docs/reference/api/overview).
- **Webex API Documentation**: [https://developer.webex.com/docs](https://developer.webex.com/docs).
