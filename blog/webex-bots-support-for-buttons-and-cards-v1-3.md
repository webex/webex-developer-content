---
type: Article
title: Webex Bots Support for Buttons and Cards v1.3
canonical_url: https://developer.webex.com/blog/webex-bots-support-for-buttons-and-cards-v1-3
content_type: blog
date: '2023-01-06'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/webex-bots-support-for-buttons-and-cards-v1-3)

Webex now supports v1.3 of the Adaptive Cards standard for bots. TL;DR: it adds support for input validation. Let's get some context on what this means by looking at building bots with buttons and cards on the Webex Developer Platform.

Remember when computer games were line-by-line text experiences? You type something, read the response, then type the next thing, and so on. That can get pretty labor-intensive. With the arrival of graphics-based operating systems, suddenly we left the world of typing behind, and started using various controllers and mice to play.

Now, just because we're working within text-based environments even today in 2022, doesn't mean we can't get creative with the User Experience (UX) provided within those spaces. In fact, when it comes to interacting with bots, it can be a much more fulfilling experience to include a sort of a little form that the user can configure and submit, instead of presenting all information and receiving all input via text alone.

### Buttons and Cards: The Adaptive Card Standard

Buttons and Cards allow for exactly this sort of dual experience when creating Webex bots. In addition to textual exchanges, bots may send a JSON object to the user that contains all the necessary information to construct a little form that users can fill out and submit right inside the chat.

Webex Engineers have made the JSON generation easier with the [Buttons &amp; Cards Designer](https://developer.webex.com/buttons-and-cards-designer) tool.

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt6be4fd30b4e35c32/63b5e9bde7947f11934147be/buttons-and-cards-designer.gif)

Using this design tool allows you to quickly configure your buttons and cards, compatible with the standard. You simply copy and paste the generated JSON into your bot's code as demonstrated in Aaron's Bitcoin Bot example.

### Buttons and Cards in Use

To really try out buttons and cards, it helps to have a bot up and running. During the [How To Build a Bitcoin Chat Bot Webinar](https://developer.webex.com/webinars), Webex Evangelist Aaron Burns gave a talk about building bots, and the code he used in his talk is a very good example of implementing a bot with cards and buttons integrated.

You can find the code from the webinar in our Webex Samples GitHub repo: [https://github.com/WebexSamples/bitcoin-bot-sample](https://github.com/WebexSamples/bitcoin-bot-sample)

Here's what the JSON for a bot card looks like in context: [https://github.com/WebexSamples/bitcoin-bot-sample/blob/main/index.js#L68-L158](https://github.com/WebexSamples/bitcoin-bot-sample/blob/main/index.js#L68-L158)

### Validation Features with v1.3

The feature that the v1.3 standard brings is implemented first on [line 93](https://github.com/WebexSamples/bitcoin-bot-sample/blob/main/index.js#L93). By utilizing the property `isRequired`, the bot developer no longer needs to add any validation code to ensure the field has been populated. This saves valuable time and allows the developer to focus on the bot functionality. The field validation will be handled by the Webex client itself and will not send the request to the bot until all the criteria has been matched.

In addition to the `isRequired` property, there are also `min`, `max`, and `regex` validators that can be added. To read more about these properties, visit the [Adaptive Cards Standards Documentation](https://learn.microsoft.com/en-us/adaptive-cards/authoring-cards/input-validation).

### Need Some Help? We Got You Covered!

We are excited to provide you with support for these v1.3 features. If you need help, the [Webex Developer Support Team](https://developer.webex.com/support) is standing by and happy to assist. You can also start or join a conversation on the Webex for [Developers Community Forum](https://cs.co/WebexDeveloperCommunity) or tweet us [@WebexDevs](https://twitter.com/WebexDevs) with your comments and requests.
