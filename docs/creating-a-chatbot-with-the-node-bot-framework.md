---
type: Guide
title: Creating a Chat Bot with the Node Bot Framework
display_title: Creating a Chat Bot
canonical_url: https://developer.webex.com/docs/creating-a-chatbot-with-the-node-bot-framework
content_type: documentation
product_group:
- webex-suite
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/creating-a-chatbot-with-the-node-bot-framework)

Learn how to create a chat bot using the Node Bot Framework.

## Introduction

In this tutorial you'll create a Webex Bot using the [Webex Node Bot Framework](https://github.com/WebexSamples/webex-node-bot-framework) and the [Webex Bot Starter](https://github.com/WebexSamples/webex-bot-starter) kit. The Node Bot Framework lets developers focus primarily on how the bot will interact with users in Webex, by writing "handlers" for various message or membership events in spaces where the bot has been added. The Webex Bot Starter is an example app that demonstrates use of the Bot Framework.

## Prerequisites

To install or run the chat bot server locally or on a remote host you will need:

* A [GitHub](https://www.github.com) account
* Git (https://git-scm.com/downloads)
* Node.js (https://nodejs.org/en/download/)

Alternatively, you can remix and configure an existing Glitch project to quickly spin up a new server. See [Deploy the Server using Webhooks](https://developer.webex.com/docs/creating-a-chatbot-with-the-node-bot-framework#deploy-the-bot-using-webhooks-optional) for details. 

## Provision a Bot

To get started you first need to provision a Bot in the Developer Portal. This involves providing a name, icon and description for your bot. In return you are provided with a **bot access token** that the Node Bot Framework server uses to make API calls on the bot's behalf.

**To provision a bot**:

1. Open the [New Bot](https://developer.webex.com/my-apps/new/bot) form on the Developer Portal.
2. Enter a name, username, and description for your bot, and select a bot icon.

    ![New bot form](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltff2e492d8ffb2754/62d07d32719eb73892496e6b/chatbot-new-bot.png)

3. Click **Add Bot**.

    A bot access token is generated. Copy and save this token for later use.

    ![Bot access token generated](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt2de504e27ddd9248/62d07d47da4a7837db52901e/chat-bot-complete.png)


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

## Add the Bot to a Space

Of course, to use the bot you created you need to add it to a space. You add a bot to a space just as you would [add a person](https://help.webex.com/en-us/article/ogreyb/Webex-App-%7C-Add-people-to-a-team-space). You can lookup the bot by its "friendly" name or username (bot@)

![Adding a bot to a space.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt25feafa9e3d05777/62d07d5374e36137c1940c19/add-bot-to-space-2.png)

Notice that when the bot is added to the space it introduces itself and provides some hints for how to use it, including a **help** command. 

![Bot introducing itself](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt54dbdfff54c3dd14/62d081d0bac71c389107b2d1/bot-added-message.png)

To get a list of commands supported by the starter bot, send it a message by mentioning it by name (@botname) followed by "help".

![Bot help command](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt470251e30aa6dca6/62d07d666dcb57349d32de33/bot-help.png)



> **Info**
>
> If your bot name contains multiple words ("Simple Chat Bot", for example) only the first word in the name is used to tag it (@Simple, for example).



## Process Incoming Messages

Most of the Node Bot Framework's functionality is based on the [framework.hears( )](https://github.com/WebexSamples/webex-node-bot-framework#Framework+hears) function. This function lets you define phrases or patterns the bot should respond to, and what actions to take in response. The code below shows the basic pattern for setting up a `framework.hears()` function.


```javascript
framework.hears(<phrase>, function(bot, trigger) {
  bot.<command>
    .then(function(returnedValue) {
      // do something with returned value
    })
    .catch(function(err) {
      // handle errors
    });
});
```

* `<phrase>` &mdash; A string or regex pattern. If a string, the string is matched against the first word in the room message. message. If a regex pattern is used, it is matched against the entire message text.
* `bot` &mdash; An instance of the [Bot class](https://github.com/WebexSamples/webex-node-bot-framework#bot) associated with the Webex space that triggered the `framework.hears()` call. You use this object to [send messages](https://github.com/WebexSamples/webex-node-bot-framework#Bot+say) to a room, [reply in-line](https://github.com/WebexSamples/webex-node-bot-framework#Bot+reply) to a message, [send direct messages](https://github.com/WebexSamples/webex-node-bot-framework#Bot+dm) and more.
* `trigger` &mdash; Provides details about the person, room, and message that caused the function to trigger.
* `bot.<command>` &mdash; The [bot method](https://github.com/WebexSamples/webex-node-bot-framework#Bot) to execute.
* `then` &mdash; (Optional) Invoked once the previous command is executed successfully.
* `catch` &mdash; (Optional) Invoked if any errors occur, either when executing the original command or in any of the chained 'then' functions.

For example, the following example listens for the phrase "hello". In response the bot sends "Hello <name>". The user's name is provided by the `trigger.person.displayName` property.

```javascript
framework.hears("hello", function(bot, trigger) {
  bot.reply(`Hello ${trigger.person.displayName}.`)
});
```

You can use a regular expression to match multiple phrases.

```javascript
framework.hears(/hello|hi|hey/i, function(bot, trigger) {
  bot.say(`Hello ${trigger.person.displayName}.`)
});
```

If multiple `hears()` handlers matches a given phrase or regex pattern, each handler is invoked in the order that it's defined in the source. This is useful for [handling unexpected input](https://developer.webex.com/docs/creating-a-chatbot-with-the-node-bot-framework#handling-unexpected-input).

## Handling Unexpected Input

If the user sends your bot a command that isn't programmed to respond to, it's good practice to provide a "catch all" `hears()` function. To do this you define a `hears()` function **after** all other `hears()` functions that matches any string (`/.*/gim`), and a state variable that indicates if the a phrase has already been handled. This works because if multiple `hears()` handlers match the same phrase or expression then the framework calls them in the order they are defined.

For example, the following shows the basic logic and structure to provide catch all message handler.

```javascript
// Initialize state variable
var responded = false;
framework.hears('hello', function(bot, trigger) {
  bot.say(`Hi ${trigger.person.displayName}`)
  // Set state variable to true
  responded = true;
});

// This will always match
framework.hears(/.*/gim, function(bot, trigger) {
  // Respond with a 'sorry' message if there wasn't a match
  if (!responded) {
    bot.say('Sorry, I don\'t know how to respond to "%s"', trigger.message.text);
  }
  // Set state variable to false
  responded = false;
});
```



> **Info**
>
> The catch-all handler **must** be the last handler defined in the source file or you will get unexpected results.



## Make a Webex API Call

Each bot instance provides a reference to a Webex JavaScript SDK instance that your app can use to make calls against that SDK. For instance, you could use [memberships.list()](https://webex.github.io/webex-js-sdk/api/#membershipslist) to get a list of members in a space so you can send each a direct message using the [bot.dm()](https://github.com/WebexSamples/webex-node-bot-framework/blob/master/README.md#Bot+dm) method, as shown below.

**To send a DM to each user in a space**:

1. Open index.js in the starter bot project.
2. Add the following code that listens for a `poke` command.

    ```javascript
    framework.hears("poke", function (bot, trigger) {
      responded = true;
      // Use the webex SDK to get the list of users in this space
      bot.webex.memberships.list({roomId: bot.room.id})
        .then((memberships) => {
          for (const member of memberships.items) {
            if (member.personId === bot.person.id) {
              // Skip myself!
              continue;
            }
            // Get name of poker
            let pokerName = (member.personDisplayName) ? member.personDisplayName : member.personEmail;
            bot.dm(member.personId, `You got poked by ${pokerName}`);
          }
        })
        .catch((e) => {
          console.error(`Call to sdk.memberships.get() failed: ${e.messages}`);
        });
    });
    ```
  
3. Save your changes and restart the Node server (`npm start`).

Once the server indicates it's listening for Webex events, send a "poke" message to the space and tag the bot by name. The bot will send a DM to each member in the space.

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
