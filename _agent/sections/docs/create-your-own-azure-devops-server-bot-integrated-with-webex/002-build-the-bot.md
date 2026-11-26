---
type: Excerpt
canonical_url: https://developer.webex.com/docs/create-your-own-azure-devops-server-bot-integrated-with-webex
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Build the Bot
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/create-your-own-azure-devops-server-bot-integrated-with-webex). [Full Markdown](../../../../docs/create-your-own-azure-devops-server-bot-integrated-with-webex.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites](001-prerequisites.md)

## Article introduction

This article explains how you can create your own Webex-integrated Azure DevOps Server bot.

## Selected section

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
