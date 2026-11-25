---
type: Excerpt
canonical_url: https://developer.webex.com/docs/creating-a-chatbot-with-the-node-bot-framework
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Process Incoming Messages
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/creating-a-chatbot-with-the-node-bot-framework). [Full Markdown](../../../../docs/creating-a-chatbot-with-the-node-bot-framework.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites](002-prerequisites.md)

## Article introduction

Learn how to create a chat bot using the Node Bot Framework.

## Selected section

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
