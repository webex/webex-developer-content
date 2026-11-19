---
type: Article
title: Introducing the Webex Bot Framework for Node.js
canonical_url: https://developer.webex.com/blog/introducing-the-webex-teams-bot-framework-for-node-js
content_type: blog
date: '2020-02-12'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/introducing-the-webex-teams-bot-framework-for-node-js)

In my [previous blog post](https://developer.webex.com/blog/from-zero-to-webex-teams-chatbot-in-15-minutes), we walked through the [Webex Bot Starter template](https://github.com/WebexSamples/webex-bot-starter) to get your very own bot running. Now, I'd like to formally introduce the open-source [Webex Bot Framework for Node.js](https://github.com/webex/webex-bot-node-framework) that we used to build the bot app, which really makes things a lot easier for bot developers.

The main idea for the framework is to make it simpler to develop [Webex bots](https://developer.webex.com/docs/bots) in Node.js. This enables you, the bot developer, to focus more on the bot and end-user experience in Webex. The project was inspired by the original [node-flint framework](https://github.com/flint-bot/flint) for Cisco Spark by Nick Marus. It simplifies building a bot app by abstracting away a lot of the complex parts of bot development, such as interacting with the API and registering webhooks. Since all that stuff is automated by the framework, you focus can be more on the interactions between the bot and your end users.

### The Sauce

In this framework, the bot's interactions can be customized by implementing "handlers" in the code, which take action on specific message or membership events in spaces where the bot has been added. The framework calls the handlers that you create to provide the essential logic of the bot.

You can create handlers for almost any event in Webex -- you can find a full list of events in the [GitHub README](https://github.com/webex/webex-bot-node-framework/blob/master/README.md#events) for the project. For instance, an important handler to use when new messages are sent to your bot is `framework.hears()` which lets you register the unique user commands that bots will listen for. Once the app *hears* a command match from the user, your app can take action by implementing a `bot.say` for example, to respond by sending a message to the space. Full details of the `bot` object and its functions can be found [here](https://github.com/webex/webex-bot-node-framework/blob/master/README.md#bot).

### Framework Support

Don't forget that you're not in this alone, fellow developer! If you have any questions, comments, or issues, we are here to assist. Click [here](https://eurl.io/#BJ7gmlSeU) to join the **Public#  Webex-Bot-Node-Framework Support** space in Webex, where you can get expert help on anything related to this framework.

In my next blog post, we'll take a deeper dive into other important functions and features of this framework, along with some tips for bot best practices, so stay tuned for more details. In the meantime, happy bot creating!
