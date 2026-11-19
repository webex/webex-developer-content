---
type: Excerpt
canonical_url: https://developer.webex.com/docs/create-your-own-google-task-bot-integrated-with-webex
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Build the Bot
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/create-your-own-google-task-bot-integrated-with-webex). [Full Markdown](../../../../docs/create-your-own-google-task-bot-integrated-with-webex.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites](001-prerequisites.md)

## Article introduction

This article explains how you can create your own Webex-integrated Google Task bot.

## Selected section

## Build the Bot

Once you have your accounts set up and Node.js installed, follow these steps to create your own Google Task bot:

1. Login to the [Google Cloud Console](https://console.cloud.google.com/).
1. Create a new project or select an existing project.
1. Navigate to **APIs &amp; Services** and then **Credentials**.
1. Select **Create Credentials** and then select **OAuth Client ID**.
1. Set the application type to **Web application**.
1. Under the **Authorized redirect URIs** section, add the URI where your application will handle the OAuth 2.0 response. This is typically your server's endpoint that handles token exchanges.
    Note down the **Client ID** and **Client Secret** for future use.
1. In the Google Cloud Console, navigate to **APIs &amp; Services** and then **Library**.
1. Search for **Google Tasks API** and enable it for your project.
1. Under APIs and Services, go to OAuth 2.0 consent screen tab, ensure you include the following scope to allow your bot to view, create, and edit tasks:
    - `https://www.googleapis.com/auth/tasks` - Full access to the user's tasks.
    - `https://www.googleapis.com/auth/tasks.readonly` - View the user's tasks.
1. Log in to <https://developer.webex.com/>.
1. Create your Webex bot at: [https://developer.webex.com/my-apps/new/bot](https://developer.webex.com/my-apps/new/bot).
1. Note down the bot's access token, which you'll use to make API requests.
