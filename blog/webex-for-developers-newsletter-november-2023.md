---
type: Article
title: Webex for Developers Newsletter – November 2023
canonical_url: https://developer.webex.com/blog/webex-for-developers-newsletter-november-2023
content_type: blog
date: '2023-11-27'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/webex-for-developers-newsletter-november-2023)

Greetings, Webex Developers! 🧑‍💻 There's been a lot of new updates and recent news to share. Let's get right to it and get caught up on everything for this month.

### 🎪WebexOne 2023: Post-Event Wrap Up!

**Webex for Developers** were well represented at the WebexOne 2023 hybrid-event in Anaheim. In a [blog post](https://developer.webex.com/blog/a-glimpse-into-webexone-2023-ai-innovations-integrations-and-more) by Developer Evangelism Leader, Adam Weeks, you can discover the highlights around the latest AI innovations and exciting new insights shared in our developer sessions.

**Webex Calling** had some exciting things to share at WebexOne, including the news of recently reaching 13 million users! To learn more about this big milestone and all the new Calling innovations that were announced, check out [this blog post](https://blog.webex.com/cloud-calling/webex-calling-at-webexone-2023/) by Director of Product Marketing, Manu Prahar.

**Webex App Hub partners** were also a big part of the AI and Future of Work showcases at WebexOne. Senior Business Development Manager, Colm McNelis, tells us all about it in [this article](https://blog.webex.com/hybrid-work/webex-integration-partners-at-webexone/).

### 📺Live Webinar: Unlocking the Power of Custom Widgets in Webex Contact Center

On *November 29 at 1:00PM EST*, join us for another [live public webinar](https://evangelism.webex.com/weblink/register/rd39ed7d28d60973471dd3724a87607f1) where we will delve into widget development for the [Webex Contact Center](https://developer.webex.com/webex-contact-center/docs), exploring key customization areas, widget types, and providing practical guidance on getting started.

As usual, head over to the [Developer Webinars page](https://developer.webex.com/webinars) to register for the live event, catch the recording later, or watch any of our previous webinars, such as the "Exploring Webex Buttons &amp; Cards" session from last month.

### 📲Advanced Calling Capabilities&#xa0;in the Webex Mobile SDK 3.10

The Mobile SDK 3.10 ([iOS](https://github.com/webex/webex-ios-sdk)) ([Android](https://github.com/webex/webex-android-sdk)) release is now available. This update adds support for up to three call transfers and brings in additional advanced Webex Calling features, which satisfies many essential mobile use cases in industries such as retail, banking and many more where customer involvement is required. Engineering Product Manager, Kriti Jain, breaks it all down in a [new blog post](https://developer.webex.com/blog/webex-mobile-sdk-3-10-advanced-calling-capabilities).

### 🔦Webex Partner Spotlight: PitchHub

We also have a [new "how-to" blog post](https://developer.webex.com/blog/dynamically-redirect-a-user-to-multiple-urls-with-webex-oauth) from Developer Evangelist, Joe Zanini, where he explores the power of dynamic redirection for Webex OAuth integrations. You will learn how you can redirect users to multiple URLs based on their behavior, preferences, or device type, which can enhance the user journey and provide valuable data for optimization.

### 🪄Dynamically Redirect a User to Multiple URLs with Webex OAuth

In a new [developer success story,](https://developer.webex.com/blog/elevating-presentations-developing-the-pitchhub-teleprompter-app-for-the-webex-app-hub) learn how Webex users can leverage a virtual teleprompter (and more) in their Webex meetings and level up presentations with the [PitchHub Teleprompter app](https://apphub.webex.com/applications/pitchhub-teleprompter-pitchhub). Also, find out how seamless the process was for them to get listed in the Webex App Hub.

### 🎥New Developer Vidcasts: Learn from the Experts!

We love watching Vidcasts that let us "skip the manual" and quickly shows how to do something. There are a couple new ones that were recently recorded for the viewing pleasure of Webex Developers:

- In [the first Vidcast](https://app.vidcast.io/share/65ca89d2-3e68-47d2-9d50-2b0909227dd3), Webex Cloud Engineer, Priya Kesari, provides a walkthrough of the Webex Web Calling SDK Kitchen Sink app.
- In [the second Vidcast](https://app.vidcast.io/share/f6bf1c22-fd18-45b6-9f8f-e67598c7bb53), Webex Product Manager, Ralf Schiffert, shows us how Service Apps can access Calling CDRs.

<br/>

### 📝Webex API Changelog Highlights

The [Webex API Changelog](https://developer.webex.com/docs/api/changelog) has several important entries listed recently and we continue to recommend checking it frequently. Here are a few noteworthy ones:

- **Nov. 12, 2023 - NEW**: The [Add Phone Numbers to a location](https://developer.webex.com/docs/api/v1/numbers/add-phone-numbers-to-a-location) endpoint now supports adding toll-free numbers via the new `numberType` field. The possible values for this field are `DID`, which is the default if not specified, and `TOLLFREE`. This functionality now properly validates that the location has a compatible PSTN connection type and ID set before adding numbers and returns an `HTTP 200 OK` rather than `HTTP 201 Created` on success.
- **Nov. 1, 2023 - NEW**: Two As indicated on September 13, here in this change log, we have now enacted the new license API with the new names and the http `PATCH`. As part of the change, we removed some license strings that had no function. These are `Webex Meetings Assistant` (WAM) and `Meeting - Webex Collaboration Meeting Rooms` (CMR).
- **Oct. 27, 2023 - NEW**: The following fields have been added to the [Webex Calling Detailed Call History report](https://developer.webex.com/docs/api/v1/reports-detailed-call-history/get-detailed-call-history): *Ring duration*, *Release time*, *Answer indicator*, *Final local*`SessionID`, and *Final remote *`SessionID`.
