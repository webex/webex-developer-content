---
type: Article
title: Webex for Developers Newsletter - End of Year 2024
canonical_url: https://developer.webex.com/blog/webex-for-developers-newsletter-december-2024
content_type: blog
date: '2024-12-02'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/webex-for-developers-newsletter-december-2024)

Greetings, Webex Developers! This edition has all the latest news as we get close to the new year. Keep reading to discover all the new updates.

### 🧑🏻‍💼The A-Z of Webex Contact Center APIs: Agents

In the latest addition to the “The A-Z of Webex Contact Center APIs” blog series, Developer Evangelist, Joe Zanini shows us how to get started building a custom desktop with the Agents APIs and the associated webhooks. He also covers the use cases for custom desktops in Webex Contact Center, pointing out where the sweet spot is for leveraging the Agent APIs.

[Read the blog  →](https://developer.webex.com/blog/the-a-z-of-webex-contact-center-apis-agents)

### 📆Create a Meeting Scheduler as a Webex Service App

In a new how-to blog post by Developer Evangelist, Phil Bellanti, learn how Webex Service Apps can automatically schedule meetings for users within an organization with a sample Python application. This will take you step-by-step for quickly creating the app and running your own demo using a developer sandbox.

[Read the blog  →](https://developer.webex.com/blog/creating-a-meeting-scheduler-as-a-webex-service-app)

### 🚛Webex Application Transfer Portal Usage Hands-on

Developer Support Engineer, Sandip Banerjee, also has a new helpful blog post that is a guide for using the Webex Application Transfer Portal. This tool allows administrators to transfer integrations, bots, service apps, and embedded apps between users within their organization. This comes in handy when someone who maintains specific apps leaves the company or assumes a new role, and a new user will be taking over the responsibility.

[Read the blog  →](https://developer.webex.com/blog/webex-application-transfer-portal-usage-hands-on)

### 🖥️Webex Developer Public Webinars

On Wednesday, January 15, 2025, at 1:00PM EST, join us for a retrospective webinar, **“Kicking off 2025 with Key Platform Advancements”**, as we look back into the exciting new features and updates introduced to the Webex for Developers platform over the past year. This session will provide developers with an overview of the enhancements designed to streamline integrations, improve user experience, and expand the capabilities of your applications. Don't miss out on this chance to elevate and stay ahead with the latest in Webex extensibility.

[Register for the live webinar  →](https://evangelism.webex.com/weblink/register/rd3b39a5fd6e46e5493a58d0b66c68635)

In case you can't make the live event, you can always watch the session recording later or check out all the past sessions on our [webinars page](https://developer.webex.com/webinars).

### 🚀Boost.space Integrates with Webex for Seamless Data Synchronization and Workflow Management

In a new partner blog post from CCO &amp; Director of Boost.space, Vít Bilinec, you will explore their powerful integration that was recently listed on the Webex App Hub. Boost.space is a data synchronization platform, and their integration allows Webex users to connect to more than 2000+ third-party applications and analyze, manage, and automate processes. The blog covers how the Boost.space app works, the developer journey on the Webex platform, and the App Hub approval process.

[Read the blog  →](https://developer.webex.com/blog/boost-space-integrates-with-webex-for-seamless-data-synchronization-and-workflow-management)

### 👩🏻‍💻Webex Recordings Downloader Demo

From time to time, there may be a need to download your past Webex Meetings recordings, which can be tedious when doing it manually one at a time. In another beneficial how-to blog post, Developer Support Engineer, Jeff Marshall, walks us through a Python application that demonstrates how an admin or compliance officer can bulk download Webex Meeting Recordings using the developer APIs.

[Read the blog  →](https://developer.webex.com/blog/webex-recordings-downloader-demo)

### 📞Developer βeta: Webex Click-to-Call

New in the Developer βeta program is Webex Click to Call, which is designed to provide a user-friendly calling experience for guest users. This powerful feature eliminates the need for downloads, accounts, and authentication, to ensure customers can connect with your enterprise effortlessly with just click of a button, improving overall customer satisfaction and engagement. Get started with early access today!

[Join the βeta  →](https://cs.co/webexdeveloperbeta)

### 📱Mobile SDK Update (iOS and Android): APIs to Boost Incoming Call Audio

In the recent Webex Mobile SDK v3.14 SDK update, receiver-side audio quality for Webex and PSTN calls can now be enhanced. This new feature results in a better overall experience for Webex Calling users when talking to non-Webex users. Check out the developer guides on the official Webex GitHub to get all the details and watch the helpful Vidcasts from our SDK engineers to get started quickly.

[Read the iOS Guide  →](https://github.com/webex/webex-ios-sdk/wiki/Bandwidth-Extension-Support)&nbsp; &nbsp; &nbsp;[Read the Android Guide  →](https://github.com/webex/webex-android-sdk/wiki/Bandwidth-Extension-Support)

[Watch iOS Vidcast  →](https://app.vidcast.io/share/d38edaff-11b0-46e7-8b3a-760830dafba3)&nbsp; &nbsp; &nbsp; [Watch Android Vidcast  →](https://app.vidcast.io/share/fa6276c2-60e8-4304-ba29-e4b124140f43)

### 🛠️Webex Contact Center: Desktop SDK Changes

Please take note of some breaking changes announced on *November 14, 2024* for the [Webex Contact Center Desktop SDK](https://developer.webex.com/webex-contact-center/docs/desktop):

- Starting on **May 16, 2025**, the JavaScript SDK will be updated to a major version where the old methods will be **deprecated** and replaced by their **newer v2 versions**. Although the functionalities will remain the same, developers need to transition to using the updated methods: `acceptV2`, `endV2()`, `cancelTaskV2()`, `pauseRecordingV2()`, `resumeRecordingV2()`, `wrapupV2()`, `consultV2()`, `consultEndV2()`, `consultConferenceV2()`, `exitConference()`, `consultTransferV2()`, `blindTransferV2()`, `vTeamTransferV2()`, and `buddyAgentsV2()`. This change is necessary to ensure compatibility and leverage the improvements made in the newer versions of these methods.
- Starting on **January 16, 2025**, the functions `Desktop.actions.getWrapUpCodes()` and `Desktop.actions.getIdleCodes()` will be **deprecated** and replaced by a paginated version of the function to fetch AUX codes. The new function, `Desktop.agentConfigJsApi.fetchPaginatedAuxCodes(\{workType, page, pageSize, search, customFilter})`, will handle the fetching of AUX codes. The `workType` parameter should be set to either `WRAP_UP_CODE` or `IDLE_CODE` to specify the type of AUX code that needs to be retrieved. This transition is part of an effort to improve the efficiency and functionality of AUX code retrieval within the system.

[Full Contact Center API Changelog  →](https://developer.webex.com/webex-contact-center/docs/api/changelog/webex-contact-center)

### 📝Webex API Recent Changelog Hits

There are also two very important changes that were recently listed in the Webex API Changelog:

- **Breaking Change - November 21, 2024:** The values of the `errorCodes` field returned by the [Get a Trunk](https://developer.webex.com/docs/api/v1/call-routing/get-a-trunk) endpoint will be changing on January 24, 2025. Please see the full changelog for the new code values. 
- **Breaking Change - November 12, 2024:** As highlighted in the [API Behavior Changes document](https://developer.webex.com/docs/app-programming-interface-behavior-changes), the `rooms/meetingInfo` API may not return information after an organization was moved to the Webex Suite Meetings Platform. As explained, the reason is that in WSMP, there is only a loose concept of a space meeting. The meeting does not happen in the space but must be scheduled via the [/meetings REST endpoints](https://developer.webex.com/docs/api/v1/meetings/create-a-meeting). The meetings REST endpoint also provides the SIP dial info for the meeting. Please utilize this REST endpoint to avoid service disruption.

[Full Webex API Changelog  →](https://developer.webex.com/docs/api/changelog)
