---
type: Article
title: Webex for Developers Newsletter – August 2023
canonical_url: https://developer.webex.com/blog/webex-for-developers-newsletter-august-2023
content_type: blog
date: '2023-08-28'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/webex-for-developers-newsletter-august-2023)

Greetings, Webex Developers! In this month's newsletter, you will find some new announcements, updates, and other interesting tidbits. So, let's dive right into the latest news to see what's happening now and looking ahead.

### ✨ New! Enhancements to the Meeting Experience

Over the next few months, all Webex meetings will start to run on our [Webex Suite meeting platform](https://help.webex.com/en-us/article/m61d8eb/Webex-App-%7C-About-the-Video-Mesh-ready-meeting-platform#reference-template_f7d2230b-bb3f-4d88-b7b5-d012273b4e4c). This allows for improved and simplified experiences for hybrid work across the entire Webex Suite, with a common architecture, administration, and integrations. To learn more about these upcoming changes and how it will affect your apps, check out this [recent blog post](https://developer.webex.com/blog/exciting-news-for-webex-developers-enhancements-to-improve-your-users-meeting-experience) by Adam Weeks.

### 📱 Webex Mobile SDK: 3.9.1 Update

In today's hyper-connected world, communication is the key to success. And to help you in this, Webex SDK 3.9.1 has just arrived, empowering your app with innovative Webex Calling features that will take your iOS or Android apps to new heights! Delve into the exciting highlights of this release and discover how it can revolutionize your mobile app's communication game with Webex Cloud Calling in [this new blog](https://developer.webex.com/blog/supercharge-your-app-with-webex-mobile-sdk-3-9-1) by Technical Leader, Hem Dutt.

### 🔦 Webex Sidebar Apps Spotlight

There has been a lot of chatter about Webex Sidebar Apps recently, which are a new type of Embedded App that exists outside of Meetings or Messaging Spaces. In a [guest blog post](https://developer.webex.com/blog/building-basicops-with-webex-sidebar-embedded-apps) by Hans Larsen from our awesome partner, BasicOps, he shows us how they built and deployed their new Webex Sidebar App and shares some helpful tips.

#### Discover More About Building Sidebar Apps

The Webex Developer Evangelism team recently hosted a live webinar on August 23rd that covered all aspects for creating [Webex Sidebar Apps](https://developer.webex.com/blog/webex-sidebar-apps). The recording of this event and (in case you missed it) the Calling API Overview from last month are now available on our [Developer Webinars page](https://developer.webex.com/webinars).

### 📞 Webex Contact Center: New Dialogflow Samples

[Google Dialogflow](https://app.use.webex.com/e/er?s=1485857328&lid=9337&elqTrackId=86ceae029ac7452a8db93a66e3e7249c&elq=8b7ff2d30b6d4ced949cfd264db16d64&elqaid=8569&elqat=1) is a natural language understanding platform that integrates with Webex Contact Center to provide advanced Interactive Voice Response (IVR) functionality. Dialogflow can be leveraged to create customized self-service call flows to better handle customer requests without involving human agents. To get started, we have some [new samples and in-depth video tutorials](https://github.com/CiscoDevNet/webex-contact-center-api-samples/tree/main/dialogflow-sample) available on GitHub, for working with data from Webex Contact Center to Google Dialogflow CX and Dialogflow ES.

### 📝 Webex API Changelog Highlights

The [Webex API Changelog](https://developer.webex.com/docs/api/changelog) has a handful of recent entries and we recommend checking it frequently. Here are a few important ones to note for this month:

- **Aug. 9th, 2023 - Breaking Change**: In the [locations API](https://developer.webex.com/docs/api/v1/locations), we will now support the field name `timeZone` instead of `timezone` to adhere to Cisco's API standards and avoid customer confusion. This change will be effective Sep 21, 2023.
- **Jul. 27th, 2023 - NEW:** A webinar host can now generate individual post-event survey links for different users using the [Get Meeting Survey Links API](https://developer.webex.com/docs/api/v1/meetings/get-meeting-survey-links) by specifying users' emails. This API only applies to webinars. Webex version 43.8.0 or higher is required.
- **Jul. 27th, 2023 - NEW:** In the [User Call Settings APIs](https://developer.webex.com/docs/api/v1/user-call-settings), new APIs have been added to [Get Users Preferred Answer Endpoint](https://developer.webex.com/docs/api/v1/user-call-settings/get-preferred-answer-endpoint) and to Modify Users Preferred Answer Endpoint. In the [Call Controls APIs](https://developer.webex.com/docs/api/v1/call-controls), the [dial](https://developer.webex.com/docs/api/v1/call-controls/dial), [answer](https://developer.webex.com/docs/api/v1/call-controls/answer), [retrieve](https://developer.webex.com/docs/api/v1/call-controls/retrieve), [pickup](https://developer.webex.com/docs/api/v1/call-controls/pickup) and [barge-in](https://developer.webex.com/docs/api/changelog#:~:text=%2C%20pickup%20and-,barge%2Din,-APIs%20have%20been) APIs have been enhanced to include an optional `endpointId` attribute.
