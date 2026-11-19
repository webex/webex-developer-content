---
type: Excerpt
canonical_url: https://developer.webex.com/docs/creating-a-chatbot-with-the-node-bot-framework
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Add the Bot to a Space
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/creating-a-chatbot-with-the-node-bot-framework). [Full Markdown](../../../../docs/creating-a-chatbot-with-the-node-bot-framework.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites](002-prerequisites.md)

## Article introduction

Learn how to create a chat bot using the Node Bot Framework.

## Selected section

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
