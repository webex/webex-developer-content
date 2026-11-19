---
type: Article
title: Webex for Developers Newsletter – March 2023
canonical_url: https://developer.webex.com/blog/webex-for-developers-newsletter-march-2023
content_type: blog
date: '2023-03-27'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/webex-for-developers-newsletter-march-2023)

Greetings, Webex Developers! We have some great info on the most recent Webex platform updates, announcements, and other interesting tidbits in this month’s newsletter. So, let's jump right in and see what's happening!

### 📺 Webinar: Getting Your App Listed on the App Hub

Coming on March 29th, Webex Developer Evangelist, Joe Zanini will host a public webinar to cover what the [Webex App Hub](https://apphub.webex.com/) is, the advantages for listing apps, and getting you smoothly through the app approval process by going step-by-step through how the submission forms should be completed.

Check out the [Developer Webinars page](https://developer.webex.com/webinars) to register for the live event or to watch the recording afterwards.

### ✨ Webex Partner Spotlight: Kaltura

At Cisco Live Amsterdam 2023, Cisco Business Development Manager, Colm McNelis sat down with Roi Etam and Hagar Schwartz from Kaltura, a provider of video solutions and content management, to talk about why the Webex platform made it easy to create a rich integration app and how it brought a holistic experience to Kaltura’s users.

You can watch the [live recorded interview on YouTube](https://www.youtube.com/watch?v=t2UfFlKuaDs) now.

### 📱Update: Mobile SDKs 3.8

Version 3.8 of the Webex Mobile SDKs for [iOS](https://github.com/webex/webex-ios-sdk/blob/master/CHANGELOG.md) and [Android](https://github.com/webex/webex-android-sdk/blob/master/CHANGELOG.md) was recently released, which includes two new features that we’re very excited about: *the meeting-only SDK*, which is a new lightweight version intended for mobile projects that are strictly using the Webex Meetings platform, and *Webex Calling support beta*, which enables mobile apps to make and receive calls from the Webex cloud.

Read more about these features in a [new blog post](https://developer.webex.com/blog/webex-mobile-sdks-3-8-0-released) from the Manager of Webex Developer Evangelism, Adam Weeks.

### 🛒 App Hub Update: New Contact Center Apps

We are pleased to announce Webex App Hub now has [Contact Center integrations](https://apphub.webex.com/contact-center) that further enable businesses to deliver intuitive customer connections in a personalized way. Come check out all the new listings in the App Hub today, such as the [NovelVox Agent Accelerator](https://apphub.webex.com/applications/novelvox-agent-accelerator) and [Eleveo WorkForce Optimization for Webex Contact Center](https://apphub.webex.com/applications/eleveo-workforce-optimization-for-webex-contact-center) integrations.

### 📊🤖 Pollbot is Now an Open-Source App

In other good news, one of the more popular Webex bot apps, [Webex Pollbot](https://apphub.webex.com/applications/pollbot-cisco-systems-12150-78220-99857), is now a freely editable [open-source project](https://github.com/WebexSamples/Pollbot-OpenSource). In [a new blog post](https://developer.webex.com/blog/pollbot-is-open-source), Developer Support Engineer, Jeff Marshall, walks us through the Pollbot functionality and how the app can be further extended. We’re looking forward to seeing what innovations can be added by our dev community!

### 🤫 Using Webhook Secrets

When setting up a webhook, developers can specify a a unique and private value that is shared between the sending and receiving apps called a *secret*. The secret is used to verify the authenticity of the request and to ensure that the request is coming from a trusted source. In a [new how-to blog post](https://developer.webex.com/blog/using-a-webhook-secret), Jeff Marshall shows us how to keep Webex webhooks locked down using the `secret` parameter.

### 💻Developer Support is Seeking Your Input

The [Webex Developer Support](https://developer.webex.com/support) team is committed to providing fast and accurate answers to your questions and help you overcome any challenges. To better serve the needs of the extensive number of users on our platform, we’ve recently transitioned from a messaging space (Webex4Dev) support model to a community forum-based model.

We’re eager to hear from you about this change - please take a quick minute to respond to [this short survey.](https://www.surveymonkey.com/r/LXS7FNW)

### 🪵 Webex API Changelog Highlights

The [Webex API Changelog](https://developer.webex.com/docs/api/changelog) has some more recent entries, so continue to keep a close on eye on it. Here are a couple important ones from this month:

- **March 7, 2023 – Breaking Change**: For security and maintainability reasons, the recordings SOAP API is deprecated **as of Jan 1, 2023**, and should not be used for any new projects. **On June 30, 2023**, the recordings SOAP API will be permanently shut down. To facilitate the migration to alternative REST APIs, two more admin-level recording report APIs are provided. As an admin user, you can now [list meeting archive summaries](https://developer.webex.com/docs/api/v1/recording-report/list-meeting-archive-summaries) with a time range on a target site and [get meeting archive details](https://developer.webex.com/docs/api/v1/recording-report/get-meeting-archive-details) with a meeting archive ID.
- **March 20, 2023 – Breaking Change**: The issue where the ['Get a List of Phone Numbers for a Person'](https://developer.webex.com/docs/api/v1/user-call-settings/get-a-list-of-phone-numbers-for-a-person) API doesn't return the&#xa0;`directNumber` in industry standard E164 format has been fixed and will be rolled out and enforced on **May 3, 2023**. Clients expecting the original format using the `GET /v1/people/{userId}/features/numbers` API may need to be updated.
