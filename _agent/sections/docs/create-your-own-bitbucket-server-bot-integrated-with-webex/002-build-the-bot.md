---
type: Excerpt
canonical_url: https://developer.webex.com/docs/create-your-own-bitbucket-server-bot-integrated-with-webex
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Build the Bot
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/create-your-own-bitbucket-server-bot-integrated-with-webex). [Full Markdown](../../../../docs/create-your-own-bitbucket-server-bot-integrated-with-webex.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites](001-prerequisites.md)

## Article introduction

This article explains how you can create your own Webex-integrated Bitbucket Server bot.

## Selected section

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
