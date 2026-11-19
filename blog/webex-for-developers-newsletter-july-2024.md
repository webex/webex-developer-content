---
type: Article
title: Webex for Developers Newsletter – July 2024
canonical_url: https://developer.webex.com/blog/webex-for-developers-newsletter-july-2024
content_type: blog
date: '2024-07-29'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/webex-for-developers-newsletter-july-2024)

Hello again, Webex Developers! We do have some interesting things to share with you this month, for both Webex and Webex Contact Center. So, relax, grab your favorite beverage, and enjoy the latest developer news for July.

### 📇The A-Z of Contact Center APIs: Address Book

The developer content for Webex Contact Center keeps rolling in! For the [first blog post](https://developer.webex.com/blog/the-a-z-of-webex-contact-center-apis-address-book) of the *A-Z series of Webex Contact Center APIs*, Developer Evangelist, Joe Zanini, focuses on the Address Book APIs. In this article, Joe goes over what the Address Book is from a user perspective, along with exploring the APIs and potential integration use cases for developers.

### 🪪Runtime Agnostic Webex OAuth for JavaScript Projects with Auth.js

In [another helpful blog post](https://developer.webex.com/blog/runtime-agnostic-webex-oauth-for-javascript-projects-with-auth-js) about getting things done easier, Ashesh Singh from the Webex Solutions Developer Team shows us how to simplify user authentication in our JavaScript applications using the new Webex OAuth provider with Auth.js. Learn how this versatile open-source authentication solution can be a great choice for JavaScript apps requiring OAuth functionality.

### 📺Webex Developer Public Webinars

*Attention Webex Calling developers!* In our most recent webinar in July, **Creating Enhanced Workflows with the Webex Calling APIs,** we presented a comprehensive overview of the entire Calling platform: APIs, use cases, and App Hub success stories. The session showcased the full developer landscape that are represented in the three pillars of Webex Calling APIs – Provisioning, Call Control, and Call Reporting - and the business value for building integrations. Check out our [webinars page](https://developer.webex.com/webinars) to watch the recording of the Calling API session. You can also find all our previous webinars or register for upcoming live sessions there.

### 📱New Developer Vidcasts: Webex Mobile SDK

The Webex Mobile SDK had some great features added in the latest update. Engineers from the Mobile SDK team recently recorded two informative Vidcasts on the new functionality that was recently released:

- Watch: [iOS SDK: External camera support overview](https://app.vidcast.io/share/6cdc9906-2693-4478-a99e-744446493fe3)
  - [Dev guide](https://github.com/webex/webex-ios-sdk/wiki/USB-Camera-Support-on-iPad)
- Watch: [Android &amp; iOS SDK: Move meeting between devices](https://app.vidcast.io/share/bd43edac-bc63-4814-b40f-eb4bc7ee2233)
  - [Dev guide](https://github.com/webex/webex-ios-sdk/wiki/Migration-to-improved-meetings-associated-with-a-space#move-meeting)

<br/>

### 🧪Webex Developer βeta Program Activity

Early adopters rejoice! The [Webex Developer Beta Program](https://developer.webex.com/docs/webex-developer-beta-program) lets you take a sneak peek and test out our upcoming features before they are released. We currently have one active beta feature you can start trying out and provide feedback on:

- Webex Web Widgets: the beta is testing password and captcha flows in Meeting and Space widgets, as well as Improved Space Meeting flows.

To get started, head over to the Developer Beta Program [information page](https://cs.co/WebexDeveloperBeta).

### 💬Unified Webex Developer Community Forum

Webex and Webex Contact Center developers now have a unified forum! We're thrilled to announce that the [Webex for Developers Community](https://cs.co/WebexDeveloperCommunity) forum has expanded to include dedicated topics for Webex Contact Center APIs and integrations. We encourage Webex Contact Center developers to utilize the combined forum to engage in discussions, exchange knowledge, and seek assistance.

### 🗓️Webex Contact Center API: Upcoming Changes

As noted in the [Contact Center API changelog](https://developer.webex.com/webex-contact-center/docs/api/changelog/webex-contact-center) on *July 10, 2024*, the scopes `cjp-analyzer:config_read` and `cjp-analyzer:read` are supported by some APIs, however since these scopes cannot be provisioned for integrations, the support for these will be removed soon. The following APIs will be affected by this change:

- [Search API](https://developer.webex.com/webex-contact-center/docs/api/v1/search/search)
- [Tasks API](https://developer.webex.com/webex-contact-center/docs/api/v1/tasks-call-control/get-tasks)
- [Get Agent Activities](https://developer.webex.com/webex-contact-center/docs/api/v1/agents/get-agent-activities)
- [Get Agent Statistics](https://developer.webex.com/webex-contact-center/docs/api/v1/agents/get-agent-statistics)
- [Get Queue Statistics](https://developer.webex.com/webex-contact-center/docs/api/v1/queue-statistics/get-queue-statistics)
- [Get Estimated Wait Time](https://developer.webex.com/webex-contact-center/docs/api/v1/estimated-wait-time/get-estimated-wait-time)

<br/>

### 📒Webex API Changelog Highlights

As usual, the [Webex API Changelog](https://developer.webex.com/docs/api/changelog) also has several recent entries and we still recommend checking this page frequently to stay up to date. Here are some latest items you can find there:

- **July 19, 2024 - NEW:** Users can obtain scheduling permissions via the [Get Scheduling Options](https://developer.webex.com/docs/api/v1/meeting-preferences/get-scheduling-options) API and update them using the [Update Scheduling Options](https://developer.webex.com/docs/api/v1/meeting-preferences/update-scheduling-options) API with the `delegateEmails` parameter. Additionally, users can add new delegate emails with the [Insert Delegate Emails](https://developer.webex.com/docs/api/v1/meeting-preferences/insert-delegate-emails) API and remove existing ones with the [Delete Delegate Emails](https://developer.webex.com/docs/api/v1/meeting-preferences/delete-delegate-emails) API.
- **June 28, 2024 – Breaking Change:** Due to security concerns the [Webex XML API](https://developer.cisco.com/docs/webex-xml-api-reference-guide/) won't support username/email+password authentication effective Nov 30, 2024 for CI native organizations (organizations managed through Control Hub only). Instead authentication must happen via the Common Identity system and the use of [session login ticket](https://developer.cisco.com/docs/webex-xml-api-reference-guide/getloginticket/#getloginticket). As a reminder the [Webex XML API has been End of Life and End of Service](https://developer.webex.com/docs/webex-xml-api-deprecation-announcement) since March 31, 2024. Some customers got an extension.
- **June 27, 2024 – Breaking Change:** Starting *August 12th, 2024*, the `callingLineId` and `routingProfile` fields will be removed from the [Test Call Routing](https://developer.webex.com/docs/api/v1/call-routing/test-call-routing) endpoint's response payload.
- **June 27, 2024 – NEW:** Starting from July 19th, 2024, a new field, `Location_ID`, will be added to the [Wholesale Billing Reports](https://developer.webex.com/docs/api/v1/wholesale-billing) API, and this applies to both Customer and User report types.
