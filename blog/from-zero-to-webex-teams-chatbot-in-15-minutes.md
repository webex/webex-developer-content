---
type: Article
title: From Zero to Webex Chatbot in 15 Minutes
canonical_url: https://developer.webex.com/blog/from-zero-to-webex-teams-chatbot-in-15-minutes
content_type: blog
date: '2023-07-19'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/from-zero-to-webex-teams-chatbot-in-15-minutes)

> **Info**
>
> This blog post was originally published in December 2019 and has now been updated for 2023.



If you are looking for the basics on how to create a Webex messaging bot, you have come to the right place. This easy to download, easy to run sample allows would-be developers to get a simple bot up and running in 15 minutes and provides a structure for building more complicated bots.

Webex currently powers thousands of bots with a variety of functionality, ranging from simple chat bots that provide specific information like the current weather, to more sophisticated bots that understand natural language and automate complex business tasks. Perhaps you've been wanting to deploy a handy chatbot of some kind and just haven't gotten a chance to start on it yet. Well, this is your big chance!

<p>
<img alt="What we're making" style="float:none" src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltdbd0d29a323c1901/5dee96c8162f1938620d47e1/bot-starter-example.gif"/>
</p>

Back when Webex (then called Spark) bot functionality was first made available, there were several simple starters. We always liked the old [sparkbotstarter](https://github.com/valgaze/sparkbotstarter) that was created by Victor Algaze, using a framework called [Flint](https://github.com/flint-bot/flint), which was created by Nick Marus. This sample is based on the updated, Webex community library [webex-node-bot-framework](https://github.com/WebexCommunity/webex-node-bot-framework), and adds a few fun new tricks, like posting a message using [Webex Buttons and Cards](https://developer.webex.com/docs/buttons-and-cards).

### Getting Started

Even if you don't have any prior knowledge of the Webex APIs, this guide will have you deploy a functioning chatbot application pretty quickly. Then from there, the bot-starter application can serve as a template for creating your own customized bots and can be extended to your heart's content. You might need to be at least a little familiar with node.js and also have the following prerequisites:

1. [Node & npm](https://nodejs.org/en/) (minimum tested version is node 8.0.0 or higher) and [git](https://git-scm.com/downloads) installed on your machine

1. A Webex account: <https://web.webex.com/>

### Sign into Webex

The first thing to do is use your regular Webex credentials to log in to Webex for Developers and create a [new bot](https://developer.webex.com/my-apps/new/bot/). When you create the bot account, be sure to jot down the bot’s username & access token before leaving the creation page - we'll need those in a minute.

### Set up the Local Web Server

The bot application has to be hosted on a server where it can communicate over HTTP. For now, we'll use [nGrok](https://ngrok.com/), which is a tool that turns your machine into a web server by opening a local port to the Internet. We're doing this so we can start using our chatbot as quickly as possible without having to think about deployment or hosting.  Since we are aiming to start testing now, nGrok uses the least number of steps to get there.



> **Warning**
>
> nGrok can open up the machine it is installed on to security risks and needs to be done only in a non-prod setup that is completely distinct from any other production services or systems. Once you’ve customized your chatbot, you should deploy it on a proper cloud hosting service, such as Microsoft Azure or other similar platforms, instead of your machine.



- Download and setup nGrok here: <https://ngrok.com/>

- After downloading and unzipping nGrok, from the same directory as the nGrok executable execute this command:

  `$ ./ngrok http 7001`

- If the tunnel has trouble connecting, try adding a region code to the command: `$ ./ngrok http 7001 --region=eu`

Once it's running, write down the web address that's tunneling to your `localhost:7001` (e.g. <https://XXXXXXX.ngrok-free.app>) and keep it handy. 

### Configure and Run the App

Now we just need to download the project, swap in a few values, and start the bot up!

- Download the [node.js Webex Bot Starter](https://github.com/WebexSamples/webex-bot-starter) template project with this command in your terminal:

  `git clone https://github.com/WebexSamples/webex-bot-starter && cd webex-bot-starter`

- From the `webex-bot-starter` directory, copy the file `.env.local` to a *new file* with only `.env` as the name. Do note these files might be hidden.

- Open the new `.env` file in a code or text editor and swap out the following values:

```json
  {
    "webhookUrl": "http://XXXXXXX.ngrok.io",
    "token": "BOT_TOKEN_CREATED_FROM_EARLIER",
    "port": 7001
  }
```

Note that if/when you turn off nGrok, when you turn it back on the URL will change and you will need to update the config with the new address.

- Save the changes to `.env` file.

- Finally, to install and start the application, run this command:

  `$ npm start`

- If you're using a Mac, you might receive a prompt asking about “node” accepting incoming network connections. If so, click **Allow** to load the server:

<p>
<img alt="incoming connection" style="float:none" src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte0e65d6d253124f6/5dee96c6aecae93859555d2f/bot-starter-incoming-connections.png"/>
</p>

### Interact with the Bot in Webex

Now that the nGrok server is loaded and the app is running, create a new group space (name the title whatever you want) in the Webex client. Next, add your bot to the space (by the username you created earlier), just as you would add any other Webex user.

If everything was done correctly, your bot should have greeted you with some instructions when it was added to the space. You now have a running chatbot! To go further, open the `index.js` file in an editor and extend functionality as much as you need.

### Helpful Resources

* This bot starter application is based from the webex-node-bot-framework:

  <https://github.com/WebexCommunity/webex-node-bot-framework>

* Intro to the Webex for Developer platform:

  [Platform Introduction](https://developer.webex.com/docs/platform-introduction)

* Webex Bots explained:

  [Bots](https://developer.webex.com/docs/bots)

* Guide for creating Webex Buttons and Cards in messages:

  [Buttons and Cards](https://developer.webex.com/docs/buttons-and-cards)
