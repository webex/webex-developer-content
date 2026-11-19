---
type: Article
title: Common Use Cases for Private Embedded Apps
canonical_url: https://developer.webex.com/blog/common-use-cases-for-private-embedded-apps
content_type: blog
date: '2022-08-08'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/common-use-cases-for-private-embedded-apps)

When you submit your Webex Embedded App to the App Hub, you are sharing it with the world. Anyone that wants to add your app to their own meetings and chat spaces can do so at will. That is not the only kind of Webex Embedded App you can build, though. Read on for some ideas.

### Reasons to Create a Private Embedded App

Why would a Developer (or their manager) decide to make a Webex Embedded App be private, instead of submitting it to the App Hub?

#### One: Avoid Limitations

When submitting an Embedded App to the App Hub, functionality of the app is limited to approved App Hub rules, limiting your app for the safety and privacy of the public. *Without*submitting your app to be listed, it *cannot* be used by the world at large; just the people in your organization. When you know your app will only be used by people in your Webex Org, you can take advantage of this extra wiggle room in what you are allowed to do with your app.

#### Two: Worry Less about Enabling PII

Personally Identifiable Information (PII) is OFF by default in all accepted Webex App Hub apps. A Control Hub Manager can set an organization’s default behavior, such that PII is on by default. Within your org, you can count on increased functionality available with PII. It is also more secure to have PII turned on in a private embedded app; the only group of people able to access the app are within the private org, limiting the attack surface.

#### Three: Additional Security

Don’t want millions of eyeballs on your app? Keep it private. By limiting the audience of your app to those within your Webex Org, you limit the scope and availability of the app’s attack surface. This does not mean that you can ignore common sense and required security accommodations. You still need to use HTTPS as your start URL, for example.

### Some Example Use Cases

Now that we understand some reasons to choose to build a Private Webex Embedded App, what are some use cases that would make sense in doing so?

#### Example One: A privately hosted instance of Jira behind a VPN

Does your company run a privately hosted app behind a VPN? You’ll be setting your custom Start URL for your embedded app to that instance, and nobody outside of your org will be able to use your app; only people on your VPN need to even see it. This is an excellent use case for a Private Webex Embedded App.

#### Example Two: A Homegrown App or an On-Premises App that You Want to Add to Meetings &amp; Spaces

Have you seen how simple it is to create a Webex Embedded App? It takes minimal effort to point to an existing URL for an app you’ve already built and add in an event handler and a couple functions. It is possible for one studious Developer to create a prototype in as little as a day.

Because all Webex Embedded Apps are private to your org unless submitted for inclusion in the App Hub, popping your existing app into your org as a Private Webex Embedded App requires minimal effort, and you don’t have to think about getting the app production-ready for global use.

#### Example Three: An App that Uses Licenses, Just Enough for Your Org

Even if your Webex Embedded App is pointed at a publicly available server, that server may only be intended for a limited number of users or may require a specific license to access. In cases where your audience is more limited than everyone-in-the-world, considering keeping your app private makes a bit of sense.

### How to Build a Private Webex Embedded App

The process to build a private app is the same as the process to build a public app. Just don’t submit it to the App Hub, and it will stay private to your Webex org.

### Wait, SHOULD I submit my app to the Webex App Hub?

Yes! In this blog, we’ve gone over some reasons and use cases related to keeping apps private, but that’s a very specific scenario. Unless you have needs mentioned in this article, you’re probably going to want to submit your app to the App Hub for broad exposure to the world.

### Summary

In short, the process of developing a Private App is no different than that of developing a public Webex Embedded App that lives in the Webex App Hub; the only thing that changes is skipping the process of submitting the app for review and inclusion in the App Hub. Developers are less restricted in what functionality they can require, such as having PII turned on. An understanding of the environment your Webex Embedded App lives within, such as the Webex Org your users are a part of, will help to make the decision.

Want to learn more about managing private Webex Embedded Apps? Read on: [https://developer.webex.com/docs/embedded-apps-guide#managing-private-embedded-apps](https://developer.webex.com/docs/embedded-apps-guide#managing-private-embedded-apps).
