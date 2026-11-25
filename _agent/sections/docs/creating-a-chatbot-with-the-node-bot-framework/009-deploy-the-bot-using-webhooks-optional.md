---
type: Excerpt
canonical_url: https://developer.webex.com/docs/creating-a-chatbot-with-the-node-bot-framework
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Deploy the Bot using Webhooks (Optional)
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/creating-a-chatbot-with-the-node-bot-framework). [Full Markdown](../../../../docs/creating-a-chatbot-with-the-node-bot-framework.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites](002-prerequisites.md)

## Article introduction

Learn how to create a chat bot using the Node Bot Framework.

## Selected section

## Deploy the Bot using Webhooks (Optional)

You've already seen it's easy to deploy a bot using websockets with the Bot Framework. Alternatively, the framework can also receive events using webhooks. Webhooks must reachable on an open port of a publicly accessible URL (note that websockets do not have this requirement). The Bot Framework makes it easy to switch between webhooks or websockets with a simple configuration change. To initiate the framework using webhooks, add a `webhookUrl` field to the framework configuration object.

```javascript
// framework options
var config = {
  webhookUrl: 'https://www.example.com/bothook',
  token: '<WEBEX_BOT_ACCESS_TOKEN>'
};
```

A slightly modified version of the Node Starter Bot is available on Glitch that you can [remix](https://glitch.com/edit/#!/remix/better-splendid-capybara) as your own. You just need to assign values to environment variables for your bot access token and webhook URL. See the [project's README](https://glitch.com/edit/#!/better-splendid-capybara?path=README.md%3A1%3A0) for setup instructions. The bot will behave identically to when it's using websockets.

[![Remix on Glitch](https://cdn.glitch.com/2703baf2-b643-4da7-ab91-7ee2a2d00b5b%2Fremix-button-v2.svg)](https://glitch.com/edit/#!/remix/better-splendid-capybara)

To use webhooks with the Node Bot Server running locally, you need to install HTTP tunneling software such as NGrok to forward webhook requests to the locally running instance. For instructions on setting up NGrok see [Setting up a Local Web Server](https://developer.webex.com/blog/from-zero-to-webex-teams-chatbot-in-15-minutes#set-up-the-local-web-server) from the [Blog From Zero to Webex Chatbot in 15 Minutes](https://developer.webex.com/blog/from-zero-to-webex-teams-chatbot-in-15-minutes).
