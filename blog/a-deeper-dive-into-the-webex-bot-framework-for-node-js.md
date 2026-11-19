---
type: Article
title: A Deeper Dive Into the Webex Bot Framework for Node.js
canonical_url: https://developer.webex.com/blog/a-deeper-dive-into-the-webex-bot-framework-for-node-js
content_type: blog
date: '2025-03-05'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/a-deeper-dive-into-the-webex-bot-framework-for-node-js)

> **Info**
>
> This blog post was originally published in February 2020 and has now been updated for 2025.



In a [previous blog post](https://developer.webex.com/blog/from-zero-to-webex-teams-chatbot-in-15-minutes), we walked through the [Webex Bot Starter template](https://github.com/WebexSamples/webex-bot-starter) to get your very own bot running. Now, we will walk through the open-source [Webex Bot Framework for Node.js](https://github.com/WebexCommunity/webex-node-bot-framework) that was used to build the demo app and really made things a lot easier.

The main idea for the framework is to make it simpler to develop [Webex bots](https://developer.webex.com/docs/bots) in Node.js. This allows you, the bot developer, to focus more on the end-user experience in Webex. It streamlines bot app development by abstracting away a lot of the complex parts, such as interacting with the API and registering webhooks. Since all that stuff is automated by the framework, you can concentrate more on the interactions between the bot and your end users. The project was originally inspired by the legacy [node-flint framework for Cisco Spark](https://github.com/flint-bot/flint) by Nick Marus.

### Framework Handlers

With this framework, the bot's interactions can be customized by implementing "handlers" in the code, which act on specific message or membership events in spaces where the bot has been added. The framework calls the handlers that you create to provide the essential logic of the bot.

You can create handlers for almost any event in Webex -- you can find a full list of events in the [GitHub README](https://github.com/WebexCommunity/webex-node-bot-framework/blob/main/README.md#events) for the project. For instance, an important handler to use when new messages are sent to your bot is `framework.hears()` which lets you register the unique user commands that bots will listen for. Once the app *hears* a command match from the user, your app can take action by implementing a `bot.say` for example, to respond by sending a message to the space. Full details of the `bot` object and its functions can be found [here](https://github.com/WebexCommunity/webex-node-bot-framework/blob/main/README.md#bot). 

### Framework Highlights

One of the best reasons to use this bot framework is to take advantage of some great built-in time saving mechanisms, allowing you to write less code. The framework gets this done by abstracting away some of the more complex Webex developer interfaces and streamlining a lot of the tedious parts of chat bot app development. 

Here are just some of the things it does automatically for you:

- Registers all the necessary webhooks (when you provide a webhook URL) or websockets (when no URL is provided)
- Finds all the spaces the bot is in without having to script multiple API calls
- Knows when a person enters or leaves a space with the bot, or when someone sends a message to the bot

The framework also makes other aspects of bot development easier, such as:

- Quickly reference details of a message and the person who sent it
- Responding with [Buttons &amp; Cards](https://developer.webex.com/docs/buttons-and-cards) without having to build the [Messages API](https://developer.webex.com/docs/api/v1/messages) call that includes attachments
- Ability to call the full range of Webex APIs from the [Webex JavaScript SDK](https://github.com/webex/webex-js-sdk)

<br/>

### Common Framework Operations

Generally, the lion's share of a bot's logic is based around responding to external events from either Webex or other systems and passing info back and forth between these systems. The framework makes it easy for developers to respond to Webex events like a new message or membership changes in spaces where the bot has been added. As a developer you need only to create a *handler* for the Webex events you are interested in. When the app runs, the framework calls the *handlers* that you created to run the essential logic of the bot.

Probably the most common handler you'll write for new messages, is `framework.hears()` which allows your bot to "listen" for your predefined commands. The command can be specified as a **string** or **regular expression**. As such, when the app *hears* a match of specific command from the user, the `framework.hears` function will be called. Then the framework passes some important parameters to that function:

- The [bot object](https://github.com/webex/webex-bot-node-framework/blob/master/README.md#bot) represents the instance of your bot in the specific space where the message was sent.
- The [trigger object](https://github.com/webex/webex-bot-node-framework/blob/master/README.md#Trigger) includes details about the message itself and the person that sent it.

The `bot` object also has functions you can call to have your bot take certain actions, for example, the `bot.say()` function can be used to send a message in the space. Full details of the bot object and its functions can be found in the [framework's documentation](https://github.com/webex/webex-bot-node-framework/blob/master/README.md#bot).

In the example below, when the bot hears the word "hello", it will respond to the user with a personalized greeting using the **trigger object** data:

```javascript
framework.hears('hello', function (bot, trigger) {
  console.log("I heard a hello.");
  bot.say('Hello, ' + trigger.person.displayName);
});
```

Another important handler is `framework.on('spawn')`, which gets called whenever your bot is added to a space. When your bot server first starts, the **spawn** handler is called for the recent spaces that your bot is already in. Afterwards, it will get called anytime someone adds your bot to a new space or if there is new activity in an older space that your bot is already in. If the `addedBy` parameter is set, it means your bot has just been added to a new space. To help you differentiate those cases, refer to the example handler below:

```javascript
framework.on('spawn', function (bot, id, addedBy) {
  if (addedBy) {
    // addedBy is the ID of the user who just added our bot to a new space,
    // Say hello, and tell users what you do!
    bot.say('Hi there, you can say hello to me.  Don\'t forget you need to mention me in a group space!');
  } else {
    // don't say anything here or your bot's spaces will get
    // spammed every time your server is restarted
    console.log('Framework created an object for an existing bot in a space called: ' + bot.room.title);
  }
});
```

Again, you can find a full list of framework events, such as the spawn event, in the [framework documentation](https://github.com/webex/webex-bot-node-framework/blob/master/README.md#spawn).

#### Using Buttons and Cards

There can also be scenarios where your bot may need to have more complex interactions with the user that would be inefficient over regular text. In cases like these, a better way for your bot to respond to a `framework.hears()` command is by sending a [card](https://developer.webex.com/docs/buttons-and-cards#working-with-cards) instead of just a text message. This can be done by calling `bot.sendCard()` in place of `bot.say()` function. This example handler sends a card in response to any input and includes markdown `fallbackText` for clients that are unable to render the card:

```javascript
framework.hears(/.*/, (bot) => {
  const fallbackText = "We just need a [few more details](https://www.example.com/form/book-vacation) to book your trip.";
  bot.sendCard(cardBody, fallbackText);
});

// define the contents of an adaptive card to collect some user input
let cardBody = {
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "version": "1.0",
  "body": [
    { ...
    }];
```

When a card includes an `Action.Submit` button, the framework will automatically generate an `attachmentAction` event whenever a user clicks on it. Applications can process these events by implementing a `framework.on('attachmentAction')` handler, like this:

```javascript
framework.on('attachmentAction', (bot, trigger) => {
  bot.say(`Got an attachmentAction:\n${JSON.stringify(trigger.attachmentAction, null, 2)}`);
});
```

The parameters passed to this hander include the `bot` object for the space where the button was clicked along with a trigger that includes an `attachmentAction` object. 

This is all demonstrated in the [buttons and cards example app](https://github.com/webex/webex-bot-node-framework/blob/master/docs/buttons-and-cards-example.md) provided as part of the framework.

### What About All the Other Webex APIs?

Although the framework and the bot objects are there to make it easy to do the most common tasks, they don't prevent you from calling the full range of Webex APIs. The framework and bot objects include an instance of the [Webex JavaScript SDK](https://github.com/webex/webex-js-sdk) which provides the functions needed for calling any of the Webex API endpoints.

For example, you might want your bot to say hello to everyone in a space. You can use the Webex JavaScript SDK to list all the members of the space to implement something like that:

```javascript
framework.hears("say hi to everyone", function (bot, trigger) {
  // Use the webex SDK to get the list of users in this space
  bot.webex.memberships.list({roomId: bot.room.id})
    .then((memberships) => {
      for (const member of memberships.items) {
        let displayName = (member.personDisplayName) ? member.personDisplayName : member.personEmail;
        bot.say('Hello ' + displayName);
      }
    });
});
```

The complete documentation for the Webex JavaScript SDK can be found here: [https://webex.github.io/webex-js-sdk/api](https://webex.github.io/webex-js-sdk/api)

### Framework Support and Community Feedback

Now that you've learned a lot about the framework, we'd love to hear about the bots you're building now or are planning to down the road. Click [here](https://eurl.io/#BJ7gmlSeU) to join the **Public Webex-Bot-Node-Framework Support** space in Webex and tell us about your cool bot ideas. You can also find help with any questions or get community support pertaining to the framework in that space.
