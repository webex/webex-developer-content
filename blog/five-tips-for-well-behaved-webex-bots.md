---
type: Article
title: Five Tips for Well-Behaved Webex Bots
canonical_url: https://developer.webex.com/blog/five-tips-for-well-behaved-webex-bots
content_type: blog
date: '2020-04-02'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/five-tips-for-well-behaved-webex-bots)

In my last few posts, we went through [deploying a simple Webex bot](https://developer.webex.com/blog/from-zero-to-webex-teams-chatbot-in-15-minutes), became familiarized with the [Webex Node.JS Bot Framework](https://developer.webex.com/blog/introducing-the-webex-teams-bot-framework-for-node-js) and then took a [deep dive](https://developer.webex.com/blog/a-deeper-dive-into-the-webex-bot-framework-for-node-js) into it. Now that we are well-versed in what goes into building a bot using the framework, let's check out a few ways you can optimize your bots to be more helpful and increase the chances that people will keep using it.  

### 1. Personalize it

Personality is important, even for bots. The closer bots can come to communicating like a real human, the more relatable they become.  Addressing users by their name can certainly be helpful in that regard, as long as it sounds natural.

You can start by having the bot introduce itself and greet the user by their name when it first gets added to a Webex space. Then have it automatically post a message to inform users what its purpose is and how they can best interact with it. You'll also want to include logic in the app so the bot does not "re-introduce" itself every time your application server restarts. This code snippet from the [Webex Bot Starter app](https://github.com/WebexSamples/webex-bot-starter/blob/master/index.js) shows how this can be accomplished:

```javascript
// A spawn event is generated when the framework finds a space with your bot in it
// If actorId is set, it means that user has just added your bot to a new space
// If not, the framework has discovered your bot in an existing space
framework.on('spawn', (bot, id, actorId) => {
  if (!actorId) {
    // don't say anything here or your bot's spaces will get
    // spammed every time your server is restarted
    console.log(`While starting up, the framework found our bot in a space called: ${bot.room.title}`);
  } else {
    // When actorId is present it means someone added your bot got added to a new space
    // Lets find out more about them..
    var msg = 'You can say `help` to get the list of words I am able to respond to.';
    bot.webex.people.get(actorId).then((user) => {
      msg = `Hello there ${user.displayName}. ${msg}`;
    }).catch((e) => {
      console.error(`Failed to lookup user details in framwork.on("spawn"): ${e.message}`);
      msg = `Hello there. ${msg}`;  
    }).finally(() =>) {
      // Say hello, and tell users what you do!
      if (bot.isDirect) {
        bot.say('markdown', msg);
      } else {
        let botName = bot.person.displayName;
        msg += `\n\nDon't forget, in order for me to see your messages in this group space, be sure to *@mention* ${botName}.`;
        bot.say('markdown', msg);
      }
    });
  }
});
```

### 2. Bot obedience

Clear and easy-to-define commands work best for bots. When using the Node.js bot framework, create a [`framework.hears()`](https://github.com/webex/webex-bot-node-framework/#frameworkhearsphrase-action-helptext-preference--string) event for each individual command. Doing it this way should make it easier for you to maintain your bot's command list and actions.  

You can even use a regular expression (regex) in the `.hears` to have the bot match a "keyword" inside of a message sent by the user with a command word. For example, if a user sends a message to the bot that says "I need help", we want the bot to recognize the keyword "hello". By using a regex in the `.hears` as shown below, the bot effectively will match the "help" command and ignore the unrecognized words "I" and "need".

```javascript
  framework.hears(/\b(\w*help\w*)\b/g function(bot, trigger){
    bot.say('Sounds like you need help! Here is how I can...');
    responded = true;
});
```

### 3. The real magic word

As shown in the previous example, the most important command that should always be implemented in a bot app is the word "help", which can respond to users with commands it can respond to or provide further instructions. It's a familiar and straightforward command - the best kind!

Your bot's introduction message may already tell users the commands it can understand, which is great. However, users can forget what those commands are. For situations like this, the bot should be able to provide clear instructions whenever it hears a "help" command from the user.

### 4. Graceful responses for all messages

Users can send all kinds of unexpected messages to your bot that may include typos, gibberish, or something you are just not expecting. Make sure your bot can respond gracefully when this occurs to perhaps remind the user of the commands it can understand. This is also a good time for the bot to show some personality.

To process user input the bot doesn't understand using the Node.js framework, you can create a "catch-all" `framework.hears` handler, using the regular expression `/*./.`:

```javascript
  let responded = false;
  framework.hears('hi', function(bot, trigger) {
    bot.say('Hi!');
    responded = true;
  });

  framework.hears(/.*/gim, function(bot, trigger) {
    // This callback will trigger on any message
    if (!responded) {
      // Only respond here if another callback hasn't already set the responded flag
      bot.say('Sorry, I don\'t know how to respond to "%s"', trigger.message.text, 'You can always say "help" if you need more instructions.');
    }
    // Reset the responded flag to false so we are ready for the next message
    responded = false;
  });
```

Note: with this example, the framework will call as many "hears" handlers that "match" the message text so this handler will be called EVERY time. Make sure you don't respond in this handler if you already responded in another one.

### 5. Optimize the user experience

Text-based bots can quickly become tedious and cumbersome for users as the bot's tasks become more complicated. Consider using [Buttons and Cards](https://developer.webex.com/docs/buttons-and-cards) instead of normal text for everything other than the most basic user interactions. *Buttons and Cards* allows users to communicate complex and multiple inputs to a bot in a singular message. It also helps bots better present information, making the important text more eye-catching and guiding users through a GUI instead of plain text.
