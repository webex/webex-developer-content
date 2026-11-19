---
type: Article
title: How to create your own RSS Feed Parser Bot for Webex
canonical_url: https://developer.webex.com/blog/how-to-create-your-own-rss-feed-parser-bot-for-webex
content_type: blog
date: '2024-12-02'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/how-to-create-your-own-rss-feed-parser-bot-for-webex)

Hello Webex Developers! If you're someone who has previously made use of the Cisco provided RSS Bot that was available through our [Webex App Hub](https://apphub.webex.com/), you're probably now aware that this bot was decommissioned recently and is no longer going to be offered. This bot was used for registering to any RSS feed out there, once there was a new feed entry it sent a notification to a Webex space of your choosing. Before it was decommissioned, the Bot sent a message to all users informing us of the same. It was a difficult decision to decommission the bot, but it had to be made due to the nature of the infrastructural changes that occurred to its dependencies which were no longer compatible with the bot and therefore we had to act.

We understand that this was not ideal for our users, and that it affected numerous applications and some automations that were reliant on it. Therefore, we thought that we should at least help our developers implement their own bot. In this blog, we'll discuss some options to get you started with your own implementation of the RSS Bot, fully customizable to tailor to your needs. We'll also share an option to immediately get you up and running, if you generally only need to follow the Webex related RSS feeds. Let's get started!

### Get updates on Webex RSS feeds right now

If you generally only ever require updates on the Webex provided RSS feeds, then this is for you. We have a ready-made option where you can simply get added to some Webex spaces that are tailor-made for our main Webex RSS feeds. There, you will get updates in real-time, as the RSS Feeds are updated. To remind you, the Webex RSS feeds are (in bold is the actual name of the Webex Space for the same):

- **Webex Incidents:** [https://status.webex.com/incidents.rss](https://status.webex.com/incidents.rss)
- **Webex Maintenance:** [https://status.webex.com/maintenances.rss](https://status.webex.com/maintenances.rss)
- **Webex Announcements:** [https://status.webex.com/updates-upgrades.rss](https://status.webex.com/updates-upgrades.rss)
- **Webex Developer API:** [https://developer.webex.com/api/content/changelog/feed](https://developer.webex.com/api/content/changelog/feed)

<br/>

#### Add yourself to the Spaces

If you want to be added to these spaces related to the above feeds, then simply follow this link: [https://eurl.io/#zE415kpu2](https://eurl.io/#zE415kpu2) and it will add the email you provide it to a Webex General Space, within a Team named **Webex RSS External**. This team contains all the Webex spaces for the above RSS feeds, named clearly to explain what RSS Feed they are for. You will be automatically added to those spaces by a bot named *TeamSync Ext* (email [teamsync.ext@webex.bot](mailto:teamsync.ext@webex.bot), you can check out its code [here](https://github.com/jeremywillans/team-sync)). You can find a screenshot of the mentioned spaces below:

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt19de2413c2ec8f5f/rss-blog-2.png)

#### How it works

The above RSS feeds are displayed in the Webex spaces thanks to a Webex Bot named *Webex RSS*, with email: [webexrss@webex.bot](mailto:webexrss@webex.bot). There is JavaScript code behind the bot that monitors the feeds for any new items and once a new item comes in it uses the bot's token to send a message to the related Webex space.

The message is simple, it just contains the feed item's title, description and web link to the online version of the same update. Based on the description of the item, it also color-codes the message on Webex: **Red** when an issue is identified (mainly used for Issue/Incident updates), **yellow** when it's being monitored or an upgrade is in progress, and **green** when issue is fixed, or an upgrade was completed successfully.

We'll explain below in more detail how the Webex RSS bot works, with code snippets taken from its repository. This should help you in building your own bot. The repository is found here, for your reference: [https://github.com/jeremywillans/webex-rss](https://github.com/jeremywillans/webex-rss). Feel free to clone it and start working on your own implementation.

### Bot Implementation Details

The production version of this bot is hosted on AWS. It uses Docker (a containerization software) to build the app container and manage it through that, then push it to an AWS service. There is a [Docker file](https://github.com/jeremywillans/webex-rss/blob/main/Dockerfile) present in the repository already for your reference. You can use that *as is* or modify it to suit your needs, if you want to deploy your own version of this bot.

The app has some environment variables that need to be configured. We usually create a `.env` file to store all these. [Here](https://github.com/jeremywillans/webex-rss/blob/main/README.md#environmental-variables) you'll find which ones are mandatory or optional, along with the default values if applicable. At minimum, if you plan to deploy your own bot you should add the bot's token and the room ID(s) you want to use for the RSS Feed updates.

The RSS feeds are configured as constants in this bot, as mentioned earlier there are 4 Webex feeds. They are hard-coded in the [app.js](https://github.com/jeremywillans/webex-rss/blob/main/app.js) file but you can add them as Environment Variables if you prefer, or even create some UI or user friendly mechanism to allow the bot's users to add their own RSS feed URLs (more on this below). And while speaking about the [app.js](https://github.com/jeremywillans/webex-rss/blob/main/app.js) file, this is where the app's logic is initiated. For the purposes of showing how this works we're just going to focus on one feed, that being the one for Webex Incidents. But all others follow pretty much the same logic, with just some minor tweaks to suit specific cases. The code samples you will see in this blog may not be the exact same as in the repository, simply because we're focusing on just one feed, but it is just slightly truncated, and all logic remains the same.

### Reviewing the Code

Initialization is done through an `init()` function. This function gets called [here](https://github.com/jeremywillans/webex-rss/blob/65879d725bfe26c7f6782765a749b4f726f626f8/app.js#L175) (and defined [here](https://github.com/jeremywillans/webex-rss/blob/65879d725bfe26c7f6782765a749b4f726f626f8/app.js#L124)) and it gets the bot details and the Webex spaces/rooms where the bot will send notifications. A `parserService` object instance exists, to call some Webex related functions such as `getBot()` and `getRoom()`. This is coming from the [parserService.js](https://github.com/jeremywillans/webex-rss/blob/main/src/parserService.js) Module we imported, we'll provide more details later on what this module does but basically its main task is to parse the feed entry we receive and format it so that we can then send a clear *RSS feed* update in the Webex Space.

You'll also see that we are using a `logger` object instance. This is just an import of the [logger.js](https://github.com/jeremywillans/webex-rss/blob/main/src/logger.js) module we've built to log any useful information of events that occur within the app. This uses the commonly known [Winston package](https://www.npmjs.com/package/winston), it is a very useful package for logging. Below is the `init()` function:

```javascript
async function init() {
  logger.info(`Webex RSS Integration, v${version}`);
  try {
    const bot = await parserService.getBot();
    logger.info(`Bot Loaded: ${bot.displayName} (${bot.emails[0]})`);
  } catch (error) {
    logger.error('ERROR: Unable to load Webex Bot, check Token.');
    logger.debug(error.message);
    process.exit(2);
  }
  try {
    const incRoom = await parserService.getRoom(env.INC_ROOM);
    logger.info(`Inc Room: ${incRoom.title}`);
  } catch (error) {
    logger.error('ERROR: Bot is not a member of the Incident Room!');
    process.exit(2);
  }
  incidentWatcher.start();
  logger.info('Startup Complete!');
}
```

### Create a Feed Watcher and Listen to Events

You'll see that we're calling `incidentWatcher.start();` This is an instance from the [feedWatcher.js](https://github.com/jeremywillans/webex-rss/blob/main/lib/feedWatcher.js) Module, it starts the watcher. This module is key as this is the logic that *watches* each feed URL and emits events once new feed entries are detected. Within this module, we first parse the feed URL to ensure it is present and usable (we import the [parseRss.js](https://github.com/jeremywillans/webex-rss/blob/main/lib/parseRss.js) module to do this. It's got some nifty code that you can look through). Then, a class named *Watcher* is defined and it extends `EventEmitter` class, which is an export from the Node.js `events` package. This is a clever way to create event listeners on the feeds, there are a number of functions such as `start(), stop(), watch()`, etc., which help to monitor the feeds for new item entries. Once a new entry is available, we process it.

A constructor is also defined to take 2 parameters, `feedUrl` and `interval` (this constructor is used to create the `incidentWatcher` instance). The `interval` parameter defines how long the watcher waits before checking the feed again for new entries. By default this bot sets the interval to 5 minutes, you can change that in [app.js](https://github.com/jeremywillans/webex-rss/blob/main/app.js) within your own implementation if you wish by changing the value of `RSS_INTERVAL` env variable (in minutes).

For the purposes of this bot, 4 `Watcher` object instances are created, aptly named to explain what they're for. We have `incidentWatcher`, `maintenanceWatcher`, `announcementWatcher` and `apiWatcher` and you'll find these in [app.js](https://github.com/jeremywillans/webex-rss/blob/main/app.js)`.` We'll mainly focus on `incidentWatcher` to explain the code flow, as they all pretty much follow the same logic, with just some minor tweaks to suit specific needs. 

To begin *watching*, the `Watcher` instance is created:

```javascript
const incidentWatcher = new Watcher(incidentFeed, interval);
```

Then we start the instance as shown previously through the `init()` function. And then we *listen*, like so:

```javascript
incidentWatcher.on('new entries', (entries) => {
  entries.forEach((item) => {
    // Identify Item Type
    logger.debug('new incident item');
    const typeIndex = item.description.indexOf('<strong >');
    if (typeIndex !== -1) {
      const typeEnd = item.description.indexOf('</strong >', typeIndex);
      const itemType = item.description.substring(typeIndex + 9, typeEnd);
      logger.debug(`detected as ${itemType}`);
      switch (itemType) {
        case 'resolved':
        case 'monitoring':
        case 'identified':
        case 'investigating':
          parserService.parseIncident(item, itemType);
          break;
        default:
          logger.debug('EVENT: UNKNOWN');
          logger.debug(item);
      }
    }
  });
```

In the above code snippet, we check for new entries (thanks to the logic from [feedWatcher.js](https://github.com/jeremywillans/webex-rss/blob/main/lib/feedWatcher.js)) and for each new entry item we find, we check the item type through a switch statement. In the switch statement we want to see whether it's an incident that's just been reported and being investigated, or root cause has been identified, or fix has been deployed and being monitored, or if it's completely resolved. These are usually the 4 stages/states of a Webex Incident.

#### Parse and Format Each Feed Entry

As we briefly touched on earlier, we have a [parserService.js](https://github.com/jeremywillans/webex-rss/blob/main/src/parserService.js) module which is used to parse any new incoming feed entry. Its main purpose is to parse the new RSS feed entry and format its content so that we can then send it as a message to the relevant Webex space. It's got a number of nested functions within the outer function named after the module it's in, that being `parserService(),` which gets exported for use elsewhere.

Some of the nested functions include: `formatDescription(), formatBlockquote(), getBot(), getRoom(), parseIncident()`, etc. They're all clearly named so it shouldn't be difficult to understand their job. They essentially combine to give you a well formatted and clear Webex message like the below one, also using some html tags to “pretty-print” the message:

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt4dedf90387d34e4f/rss-blog-3.png)

#### Handle Feed Errors and Stop the Watcher

The bot has logic that checks for any possible errors with the feed (for example, if the feed URL is down). Code is simple but effective, see below:

```javascript
incidentWatcher.on('error', (error) => {
  logger.error(`Inc Feed Error: ${error}`);
});
```

We also handle graceful shutdown through SIGINT and stop the watcher at that point, see below:

```javascript
process.on('SIGINT', () => {
  logger.debug('Stopping...');
  incidentWatcher.stop();
  logger.debug('Feeds Stopped.');
  process.exit(0);
});
```

#### Send Webex Messages

To send the Webex messages to each space, we've got the [httpService.js](https://github.com/jeremywillans/webex-rss/blob/main/src/httpService.js) Module. We import the [axios](https://www.npmjs.com/package/axios) npm package to aid this, it is a very useful package for sending HTTP Requests to RESTful APIs, such as ours. What I like most about Axios is that it also comes with additional packages [axios-retry](https://www.npmjs.com/package/axios-retry) to retry API calls as required, and [axios-rate-limit](https://www.npmjs.com/package/axios-rate-limit) to manage the API's rate-limiting by adding a timeout. These help developers manage API requests properly, ensuring minimal disruptions due to the API's rate-limiting policies and other issues that may require retries.

The main function in this module is the `postMessage()` function. As the name suggests, this function posts the message to the related Webex space, using the [https://webexapis.com/v1/messages](https://webexapis.com/v1/messages) API (documented [here](https://developer.webex.com/docs/api/v1/messages/create-a-message)). This API requires a `roomId` (for group spaces/rooms) or one of `toPersonId` or `toPersonEmail`, if you want to send a direct/1:1 message. The bot only sends messages to group spaces/rooms in its current configuration, but it does have code within this function to handle cases where direct messages are sent. Below is the code snippet showing the initial POST request's `options` object being created and also the if/else statement handling the message type:

```javascript
return new Promise((resolve, reject) => {
  const directMessage = direct || false;
  const messageFormat = format || 'html';
  const options = {
    method: 'POST',
    url: 'https://webexapis.com/v1/messages',
    headers: {
      authorization: `Bearer ${accessToken}`,
      'Content-Type': 'application/json',
    },
    data: {},
    json: true,
  };
  if (directMessage) {
    options.data.toPersonId = destId;
  } else {
    options.data.roomId = destId;
  }
  // ...
});
```

As you can see, the `options` object contains the `method`, `url`, `headers`, `data` and `json` properties. Our request body will go in the `data` property, and with the following if/else statement we define whether to use `roomId` or `toPersonId.`

Beyond this, the API also requires the `text` or `markdown` fields to be passed in its request body. The bot only sends `markdown` messages given that it's formatting the message, below is code for how it adds it to the `data` property within `options`, in the same function:

```javascript
options.data[messageFormat] = message;
if (messageFormat === 'markdown') {
  options.data[messageFormat] = message.replace(/\\n/g, '\n');
}
```

Now, we send the request with `axios`. Here's how we build the request:

```javascript
axios
    .request(options)
    .then((response) => {
      // Check JSON payload is compliant with specs
      if (!response.data) {
        logger.debug('could not parse message details: bad or invalid json payload.');
        reject(response.status);
      }
      logger.debug('message sent');
      resolve();
    })
    .catch((error) => {
      logger.debug(`postMessage error: ${error.message}`);
      if (error.response &amp;&amp; error.response.headers.trackingid) {
        logger.debug(`tid: ${error.response.headers.trackingid}`);
      }
      reject(error);
    });
```

There we go! This should now post your message with the feed update to the space, so we've gone through the full basic flow of the app. And just to complete explaining this module, there is another function called `getField()`. Its main task is to do a `GET` to one of our APIs (which one exactly is determined by an `apiName` param we send in when calling the function). It's called twice in the [parserService.js](https://github.com/jeremywillans/webex-rss/blob/main/src/parserService.js) Module, once each in the `getBot()` and `getRoom()` functions, and it's a nice example to showcase how the same code can get reused multiple times. You can use this in other `GET` requests if needed, where you need to do a GET to our APIs. Just send the `token` and `apiName` params (for example `/rooms` or `/people` API string names) and the function should take care of the request for you.

### What if You Want to Use Non-Webex RSS Feeds?

We've got you covered. We've simplified the code above into this [Boilerplate template RSS Bot](https://github.com/WebexSamples/Boilerplate-RSS-bot) so that you just have to add your own feed URL, bot token and room ID as environment variables. You can then run the bot in your own environment and it should respond with a simple message that includes the feed item's title, description and link (do make sure that your Feed URL has said properties. If not change them in the code).

We've basically stripped down the code we've talked about above, so a lot of the formatting has been removed as well as some *feed-specific* code logic. It still does some minor formatting on the message but to a much lesser extent than what the code above has. The code logic remains very much the same, just simplified to make it easier to get started with your own implementation.

To give you a view of what a message from this boilerplate code sample would look like, here is an image showcasing the same (we used a basic test RSS feed, so the content is just some *lorem ipsum* text, but you get the idea):

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt677f93294dbe2fbc/rss-blog-4.png)

### Allow users to add their own RSS Feed URL

If you plan on building a sort of (or maybe even fully fledged) Production bot to cater for this use case, you may want to give users the option of adding their own RSS Feed URLs, instead of *hard-coding* them in the code. There are several ways to manage this, for example you could build a web UI where users can enter some initial details such as room ID, Feed URL, etc., and then you can store those in a database so that your bot can reference those later when working with said users. You could also add some additional logic with a [Webex OAuth Integration](https://developer.webex.com/docs/integrations), where the user authorizes this integration through your UI and the resulting access token created from that can be used to pull all the user's spaces, to give them a dropdown option (or similar UI option), allowing them to choose which space to add the bot to and set up the RSS feed notifications for. This would be somewhat like what the old RSS bot did, if you liked that process then this might be something to work on.

Or you might want to keep it a bit simpler than that. In that case, you may want to try using [Adaptive Cards](https://developer.webex.com/docs/buttons-and-cards) with your bot. You could create logic where the bot sends an adaptive card to a space they just got added to, to allow the user to add some details like the RSS feed URL they want to use and then you store it on your side. You will need to add some kind of listener to *listen* to any membership creations on the bot. You have 2 ways to manage this:

1. By creating a [Webhook](https://developer.webex.com/docs/webhooks) using the bot's token, on the `memberships` resource with the `created` event.
1. By Creating a [Websocket](https://developer.webex.com/blog/using-websockets-with-the-webex-javascript-sdk) using the bot's token within our [JavaScript SDK](https://developer.webex.com/docs/sdks/browser), on the same resource and event.

The difference between these is that websockets are generally used when you do not want to use a public server URL, for example if you're working behind a firewall or other network restrictions. Whereas webhooks need a public URL (with no auth requirements) to be defined as the `targetURL,` that's where the webhook payload is sent. In any case, whichever option you decide to use, once the listener gets triggered you can then send an adaptive card that has some options that the user can fill in. As a visual example, here is a very simple one that looks like this:

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt5b0aeacf6884a683/rss-blog-5.png)

The JSON for this is below:

```json
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "version": "1.3",
  "body": [
    {
      "type": "ColumnSet",
      "columns": [
        {
          "type": "Column",
          "width": 2,
          "items": [
            {
              "type": "TextBlock",
              "text": "Register your RSS Feed notification",
              "weight": "Bolder",
              "size": "Medium"
            },
            {
              "type": "TextBlock",
              "text": "Enter URL",
              "wrap": true
            },
            {
              "type": "Input.Text",
              "id": "myName",
              "placeholder": "Feed URL"
            }
          ]
        }
      ]
    }
  ],
  "actions": [
    {
      "type": "Action.Submit",
      "title": "Submit"
    }
  ]
}
```

Adaptive cards are explained in detail [here](https://developer.webex.com/docs/buttons-and-cards), with some samples too. Worth a read if you've never used them before. We also have the [Buttons and Cards Designer](https://developer.webex.com/buttons-and-cards-designer) to build your own card if you wish. Ours above is quite basic, there are many more options you can use to make it more visually (and functionally) appealing. The basic (pseudo) flow works like this:

1. First, create a Webhook (or websocket) on the `attachmentActions` resource, same way as we discussed earlier.
1. This gets triggered every time someone interacts with an action on your card.
1. In the above case, the action is the **Submit** button, the JSON contains an `actions` array with a `Action.Submit` type. That's your action.
1. Once the user enters their RSS feed and submits, your webhook/websocket gets triggered and you can then proceed with registering the notification set up for them.

The code samples we've explained in this blog don't currently have any of this functionality, but we thought we should at least mention how you can go about it if you plan on doing something like this.

Furthermore, to scale this app you'll likely have to store some information. What you store and how/where you store it is up to you. A viable approach might be to use a DB to store the RSS feed URL the user entered, along with some other details such as the roomId (the `memberships` webhook/websocket returns that) and maybe some user data to identify the user who created the notification so you can match it to that user every time that's required in your flow. Of course, you should ensure there are no legal ramifications with the data you may decide to store (most notably any user data).

And that's that, We hope this helps!

### Need Some Help? We Got You Covered!

As always, should you have any queries about this or any other Webex Developer related topics, please don't hesitate to reach out to our team. We're dedicated to helping developers wherever possible, any time. You can reach out through the [Webex Developer Support channels](https://developer.webex.com/support) 24/7.

Happy coding!
**The Webex Developer Team**
