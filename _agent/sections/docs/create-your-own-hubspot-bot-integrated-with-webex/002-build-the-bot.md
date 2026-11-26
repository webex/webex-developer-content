---
type: Excerpt
canonical_url: https://developer.webex.com/docs/create-your-own-hubspot-bot-integrated-with-webex
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Build the Bot
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/create-your-own-hubspot-bot-integrated-with-webex). [Full Markdown](../../../../docs/create-your-own-hubspot-bot-integrated-with-webex.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites](001-prerequisites.md)

## Article introduction

This article explains how you can create your own Webex-integrated HubSpot bot.

## Selected section

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
