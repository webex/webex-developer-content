---
type: Excerpt
canonical_url: https://developer.webex.com/docs/create-your-own-trello-bot-integrated-with-webex
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Build the Bot
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/create-your-own-trello-bot-integrated-with-webex). [Full Markdown](../../../../docs/create-your-own-trello-bot-integrated-with-webex.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites](001-prerequisites.md)

## Article introduction

Follow the instructions in this article to create your own Trello bot for Webex.

## Selected section

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
