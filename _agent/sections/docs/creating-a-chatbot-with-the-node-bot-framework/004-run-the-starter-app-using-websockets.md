---
type: Excerpt
canonical_url: https://developer.webex.com/docs/creating-a-chatbot-with-the-node-bot-framework
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Run the Starter App Using Websockets
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/creating-a-chatbot-with-the-node-bot-framework). [Full Markdown](../../../../docs/creating-a-chatbot-with-the-node-bot-framework.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites](002-prerequisites.md)

## Article introduction

Learn how to create a chat bot using the Node Bot Framework.

## Selected section

## Run the Starter App Using Websockets

You can run the Node Bot server in "websocket" mode on your local system, without having to deploy a public service (or configure reverse proxies required for webhooks running on your local system). If the configuration object you pass to the Framework constructor function doesn't contain a `webhookUrl` field, the framework falls back automatically to websockets. Even if you don't intend to use websockets in your production bot service, it provides a quick way to start creating and testing.

You will need the bot access token [generated previously](https://developer.webex.com/docs/creating-a-chatbot-with-the-node-bot-framework#provisioning-a-bot) to complete this section.

**To run the starter app in websocket mode**:

1. Clone the [Webex Bot Starter](https://github.com/WebexSamples/webex-bot-starter) repository.

    ```bash
    git clone https://github.com/WebexSamples/webex-bot-starter.git
    ```

2. Rename `config-template.json` to `config.json`. This file contains configuration options for the Node Bot Framework.
3. Replace the contents of config.json with the following, replacing `<BOT_ACCESS_TOKEN>` with your bot's access token.

    ```javascript
    {
      "token": "<BOT_ACCESS_TOKEN>"
    }
    ```

4. Start the server (also installs packages):

    ```bash
    npm start
    ...
    Starting framework, please wait...
    Listening for webex teams events...
    framework is all fired up! [Press CTRL-C to quit]
    ```
