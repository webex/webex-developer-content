---
type: Article
title: Word of The Hour Bot on Webex
canonical_url: https://developer.webex.com/blog/word-of-the-hour-bot-on-webex
content_type: blog
date: '2022-04-07'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/word-of-the-hour-bot-on-webex)

### Introduction

As an independent developer, I actively seek out new platforms to build and launch applications. If you are an engineer who ventures outside of the common web and mobile development platforms, you will find alternative platforms that need talented independent developers who can help satisfy customer needs, build new brands, and advance new market opportunities.

#### My Question

This need for independent developers led me to the following question: “*What platforms should independent developers be looking at in 2022 and beyond?”*

#### One Possible Answer

I suggest that the answer may very well be integrations, addons, and bots for chat and messaging platforms. Therefore: “*With the recent growth in remote and hybrid work opportunities, chat and messaging platforms have become essential within the workplace which has introduced new challenges and opportunities.** **If an addon can help increase productivity, improve quality of collaboration, or advance education, then there will be an immediate benefit for a customer or business.”*

### Word of The Hour

For the past five years, I have been developing a multiplatform application called [Word of The Hour](https://wordofthehour.org/) (or WOTH). WOTH allows users to learn 24 new vocabulary words every day (or one word per hour) across over 10+ languages including (Spanish, French, German, Italian, Portuguese, Welsh, Swedish, and more!). WOTH is intended to be a supplement to your language learning experience by providing additional vocabulary practice, notifications, and motivation to stay active with your language education. For more information about WOTH, see our website [here](https://wordofthehour.org/).

Recently, WOTH has started working with world leading messaging platforms to pursue new and innovative opportunities. Naturally, Webex has been a key platform to focus on.

### Developing for Webex Platform

The [Webex](https://www.webex.com/) platform stood out to me because of its focus on professionalism, innovation, and language accessibility. So let us talk briefly about how I got started with developing WOTH for Webex.

For Webex, you can develop Bots or Integrations. A bot is like a Webex user that can communicate with you via messaging. On the other hand, an integration is more like an external application that can connect with your Webex account.

Below I will talk about how I built a bot for the Webex platform:

1. Go to the [Webex for Developers Website](https://developer.webex.com/). Create a Webex account and then select "Start Building Apps".
    From there, you can create your bot and obtain a bot username (for example, my bot's username is WordOfTheHour@webex.bot). Users will be able to communicate with the bot directly or by adding the bot to an existing space.
1. Start building the bot. I decided to build the WOTH bot using [Node.js](https://nodejs.org/).
Get started by cloning the Git repository: [Webex Node Bot Framework](https://github.com/WebexCommunity/webex-node-bot-framework). Look at the README.md file for instructions on Installation and Examples. I also decided to have the WOTH bot reply with [Buttons and Cards](https://developer.webex.com/docs/buttons-and-cards).
    When developing your bot, I strongly encourage you to carefully read through Webex's documentation to see how features are supported across all Webex client applications.
1. Once I had a demo ready, I started testing locally. To do this, I created an account with [nGrok](https://ngrok.com/). Next, I was able to configure the WOTH bot with the appropriate nGrok URL and port number. Then, I could run my Node.js application to see my bot interacting with the Webex platform.
    Later, I deployed my Node.js application onto a [Heroku](https://www.heroku.com/) server and changed the configuration to use the appropriate Heroku URL and port number.
1. The final step is to launch your creation to the [AppHub](https://apphub.webex.com/). This will allow Webex users to be able to find your creation and get started using it.
    As an example, see the AppHub page for Word of The Hour [here](https://apphub.webex.com/applications/wordofthehour-word-of-the-hour-66032). Also, give the WOTH bot a try. It is currently in its initial version, but we are hoping to gain feedback and add additional features soon!

Thank you for reading and I hope that you will consider developing applications for chat and messaging platforms like Webex!
