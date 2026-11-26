---
type: Excerpt
canonical_url: https://developer.webex.com/docs/creating-a-chatbot-with-the-node-bot-framework
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Handling Unexpected Input
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/creating-a-chatbot-with-the-node-bot-framework). [Full Markdown](../../../../docs/creating-a-chatbot-with-the-node-bot-framework.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites](002-prerequisites.md)

## Article introduction

Learn how to create a chat bot using the Node Bot Framework.

## Selected section

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
