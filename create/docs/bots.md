---
type: Guide
title: Bots
display_title: Bots
canonical_url: https://developer.webex.com/docs/bots
content_type: documentation
product_group:
- webex-suite
categories:
- app-hub
- create
- messaging
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/bots)

Give Webex users access to outside services right from their Webex spaces. Bots help users automate tasks, bring external content into the discussion, and gain efficiencies.

[Create a Bot](<https://developer.webex.com/my-apps/new/bot>)

## Bots Explained

Bots are similar to regular Webex users. They can participate in 1-to-1 and group spaces and users can message them directly or add them to a group space. A special badge is added to a bot's avatar in the Webex clients so users know they're interacting with a bot instead of a human.

A bot can only access messages sent to it directly. In group spaces, bots must be [@mentioned](https://help.webex.com/p5k20o/) to access the message. In 1-to-1 spaces, a bot has access to all messages from the user.

Bots do not, however, perform actions within Webex on behalf of a Webex user. If you're creating an application that needs to participate in Webex and perform actions with a user's account, check out [Integrations](https://developer.webex.com/docs/integrations).

## Types of Bots

Bots come in all different shapes and sizes. Here are some ideas for a few different types of bots you can make:

### Notifiers

Notifier bots typically respond to events in external services and post a summary in Webex. For example, a _GitHub Bot_ may listen for commits on a particular repo and post the committer's name and comment into a Webex space set aside for this purpose. Or a _Deal Bot_ that lives in an account-specific space and posts updates from a CRM along with relevant news about the company like a product launch or earnings report.

### Controllers

Controller bots act as a text-based remote control for external services. For example, a _Jira Bot_ may allow software engineers and product managers to control or query information from the popular bug tracking system Jira, all from the comfort of a Webex space.

<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt15175555e3f933b0/5d4ad4ec0331293861b7a626/Bot-Example.png" width="500" height="245" title="Controller Bot"></img>

Controller bots are generally passive, waiting for someone in the room to issue a command. In group rooms, bots can only see messages in which they are mentioned (1:1 rooms bots can see all messages as they are automatically "mentioned"). Your users are required to mention the bot preceding the command like `@jira find WEBSITE-22` where `@jira` is the bot's name.

Currently, the Webex SDKs do not support extracting commands from messages. You'll need to parse it out after the mention. Future versions of the Webex SDKs will have built-in support for commands. Keep your eyes on the blog for updates.

### Assistants

Virtual assistants are the holy grail of chatbots. At minimum, an assistant should understand natural language, allowing the user to ask it questions as they would to a human.

Recent advancements in NLP (Natural Language Processing) have made understanding natural language requests not only possible, but quite accessible to the average developer. Most notably, Google launched [Google Cloud Natural Language API](https://cloud.google.com/natural-language/) in the summer of 2016, providing syntax parsing, sentiment analysis and deep noun classification.

Responding to natural language is a good first step but a truly exceptional assistant bot will be conversational, using past interactions to contextualize the most recent query. This is a very complex problem domain; luckily there are companies like [Dialogflow](https://dialogflow.com/) providing a conversational platform built specifically for bots.

## Creating a Webex Bot

Creating a Webex Bot is super easy. If you're logged in, select [My Webex Apps](https://developer.webex.com/my-apps) from the menu under your avatar at the top of this page, click "Create a New App" then "Create a Bot" to start the wizard.

You'll be asked to provide some basic information about the bot: bot name, bot username, and an icon. These fields are end-user facing, so make them as descriptive as possible. Only the bot's first name will be shown when mentioned in messages, so try to avoid spaces in the bot name.  The description will be shown to users if you submit your bot to the [Webex App Hub](https://developer.webex.com/docs/app-hub-submission-process).



> **Warning**
>
> Webex App Hub is not supported for Webex for Government (FedRAMP)



Once you've filled out the registration form click "Add Bot", and if everything goes smoothly you're all set! You'll be given an access token for the new bot. This access token will be used to authenticate your bot with the Webex REST API.



> **Warning**
>
> The bot's access token will only be displayed once. Make sure to scroll down on the confirmation page, copy the token and keep it somewhere safe. If you misplace it, you can always generate a new one by finding the bot in [My Webex Apps](https://developer.webex.com/my-apps) and selecting "Regenerate Access Token" from the edit page.



## Responding to Events

After creating a bot, you can use its access token with the Webex REST APIs to perform actions as the bot, such as [sending a message](https://developer.webex.com/docs/api/v1/messages/create-a-message) with an interactive [card](https://developer.webex.com/docs/buttons-and-cards) to someone. To respond to events within Webex, such as someone sending your bot a message or adding it to a group space, you'll need to configure webhooks. Webhooks will let you know when an activity has occurred so you can take action. Check out the [Webhooks Guide](https://developer.webex.com/docs/webhooks) for more information about configuring webhooks.

With cards, you can give your users even more ways to interact with your bot or service, right in the Webex clients. Use the [Buttons and Cards Designer](https://developer.webex.com/buttons-and-cards-designer) to quickly create and prototype cards for your bot. See the [Buttons and Cards Guide](https://developer.webex.com/docs/buttons-and-cards) for more information about cards.

## Differences Between Bots and People

One key difference between Webex Bots and regular users is that, in group spaces, bots **only have access to messages in which they are mentioned**. This means that `messages:created` webhooks only fire when the bot is mentioned in a space. However bots are on the roster of a space and they do have encryption keys for the space so the pattern of using mentions does not protect other messages in the space from being accessed by a bot in all flows.

Also, [listing messages](https://developer.webex.com/docs/api/v1/messages/list-messages) requires that you specify a special `?mentionedPeople=me` query parameter.

In addition people have a `personId` that must be resolved via /people, bots have a Bot Id and a `personId`. The Bot Id is shown in the apps page and is usually only known to the developer. The bot's `personId` can be looked up via the bot's email address in /people. 

```http
GET /messages?mentionedPeople=me&roomId=SOME_INTERESTING_ROOM
Authorization: Bearer THE_BOTS_ACCESS_TOKEN
```

## Bot Frameworks & Tools

There are several bot frameworks that can greatly simplify the bot development process by abstracting away the low-level communications with the Webex REST API, such as creating and sending API requests and configuring webhooks. Instead, you can focus on the building the interaction and business logic of your bot.

[Flint](https://github.com/flint-bot/flint) is an open source bot framework with support for regex pattern matching for messages and more.

[Botkit](https://github.com/howdyai/botkit) is a popular open source bot framework with advanced conversational support as well as integrations with a comprehensive array of natural language processing and storage providers. You can get started with Botkit by cloning the Webex [Botkit Starter Kit](https://github.com/howdyai/botkit-starter-ciscospark).

The Cisco Webex Ambassador program has links to several more [open source bot starter kits](https://ciscowebexteamsambassadors.github.io/StarterKits/). Keep your eyes on our [blog](https://developer.webex.com/blog) for updates and news about our community-supported tools!
