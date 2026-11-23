---
type: Excerpt
canonical_url: https://developer.webex.com/docs/create-your-own-wrike-bot-integrated-with-webex
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Build the Bot
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/create-your-own-wrike-bot-integrated-with-webex). [Full Markdown](../../../../docs/create-your-own-wrike-bot-integrated-with-webex.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites](001-prerequisites.md)

## Article introduction

This article explains how you can create your own Webex-integrated Wrike bot.

## Selected section

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
