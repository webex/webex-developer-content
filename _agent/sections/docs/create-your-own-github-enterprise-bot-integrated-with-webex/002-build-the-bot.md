---
type: Excerpt
canonical_url: https://developer.webex.com/docs/create-your-own-github-enterprise-bot-integrated-with-webex
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Build the Bot
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/create-your-own-github-enterprise-bot-integrated-with-webex). [Full Markdown](../../../../docs/create-your-own-github-enterprise-bot-integrated-with-webex.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites](001-prerequisites.md)

## Article introduction

This article explains how you can create your own Webex-integrated GitHub Enterprise bot.

## Selected section

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
