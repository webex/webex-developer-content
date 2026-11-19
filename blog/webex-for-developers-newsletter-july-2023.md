---
type: Article
title: Webex for Developers Newsletter – July 2023
canonical_url: https://developer.webex.com/blog/webex-for-developers-newsletter-july-2023
content_type: blog
date: '2023-07-26'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/webex-for-developers-newsletter-july-2023)

Greetings, Webex Developers! In this month's newsletter, you will find some new announcements, updates, and other interesting tidbits. So, let's dive right into the latest news to see what's happening now and looking ahead.

### 📺Live Webinar: Webex Calling Provisioning APIs

Lately, we’ve seen an uptick in demand for more Webex Calling API learning content, to take advantage of the great new endpoints that recently have been made available. To answer those “calls”, we are pleased to announce our next public webinar on Wednesday, July 26th at 1:00PM EDT, where the Developer Evangelism and Product teams walk us through the world of Webex Calling Provisioning APIs. [Register](https://developer.webex.com/webinars) for the live event now or [watch](https://developer.webex.com/webinars) the recording later.

### 🦄The WebRTC Story – An Introduction to WebRTC

When it comes to building multimedia apps, we hear the term “WebRTC” mentioned quite a bit. Many folks are now asking: *what exactly is WebRTC and what does it do*? In a [recent blog post](https://developer.webex.com/blog/the-webrtc-story-an-introduction-to-webrtc), Software Engineer, Kesava Krishnan Madavan, tells an interesting story about the WebRTC protocol and the concept of how it works. A good read for everyone who wants to get know this important technology.

### 🃏Webex Buttons &amp; Cards: Enhanced Accessibility

In today's digital age, accessibility is a key aspect of creating inclusive and user-friendly experiences. Webex Software Engineer, Urmit Chauhan, explains in another [new blog post](https://developer.webex.com/blog/buttons-and-cards-enhancing-visual-focus-accessibility) how recent improvements in Webex Buttons &amp; Cards have made it easier for bot developers to provide users with a delightful accessibility experience in [Messaging](https://www.webex.com/suite/messaging.html).

### 🤖Refreshed for 2023: Build a Webex Chatbot in 15 Minutes

One of the more popular Webex Developer blog posts, particularly for beginners, has been updated for 2023: [From Zero to Webex Chatbot in 15 Minutes](https://developer.webex.com/blog/from-zero-to-webex-teams-chatbot-in-15-minutes). In this blog, Developer Evangelist, Phil Bellanti, takes us step-by-step to quickly create &amp; deploy a messaging bot app, that also provides a structure for building your own. Surprise your colleagues with a helpful bot that was designed by you!

### 🎪WebexOne 2023: Big Ideas. Bold Innovations. A New Experience

On October 24-26 at the Anaheim, CA Marriott, join us for [WebexOne 2023](https://www.webexone.com/), which will be a first of its kind hybrid event that you won’t want to miss. Be at the forefront as we unveil new innovations in hybrid work and customer experience. Share ideas, collaborate on projects, and build a network of peers who can support your professional growth. Take part of the training sessions that offer valuable learning content. [Register](https://www.webexone.com/) for your spot today!

### 🪵Webex API Changelog Highlights

The [Webex API Changelog](https://developer.webex.com/docs/api/changelog) has a bunch of new entries that you will want to take note of and we recommend to continue to check there frequently. Here are some of the recent updates listed:

- **June 28, 2023 – NEW:** We do now support limited HTML markup in [message creation](https://developer.webex.com/docs/api/v1/messages/create-a-message) and edits. The supported HTML tags are limited to `h1`,`h2`,`h3`,`ul`,`ol`,`u`,`i`,`b` and `href` links.
- **June 28, 2023 – NEW:** Webex Calling [detailed call history API CDR feed](https://developer.webex.com/docs/api/v1/reports-detailed-call-history/get-detailed-call-history) is included with additional "Reasons" and "User type" attributes, clarifying user types and call reasons that can be initiated, terminated, or redirected. For more details about these new attributes see [Detailed call history API](https://developer.webex.com/docs/api/v1/reports-detailed-call-history), or [Webex Calling reports for your collaboration portfolio.](https://help.webex.com/en-us/article/nmug598/Reports-for-Your-Cloud-Collaboration-Portfolio)
- **July 6, 2023 – NEW:** We've added support for an "announcement repository", which is a centralized repository of media at the customer/org and location levels. Different features can utilize this media for things like audible announcements being played when certain events/situations happen. The following APIs can upload and list announcements at the customer or org level:
  - [Upload a binary announcement greeting at organization level](https://developer.webex.com/docs/api/v1/webex-calling-organization-settings-with-announcements-repository-feature/upload-a-binary-announcement-greeting-at-organization-level)
  - [Fetch list of announcement greetings on location and organization level](https://developer.webex.com/docs/api/v1/webex-calling-organization-settings-with-announcements-repository-feature/fetch-list-of-announcement-greetings-on-location-and-organization-level)
  - [Fetch details of binary announcement greeting at organization level](https://developer.webex.com/docs/api/v1/webex-calling-organization-settings-with-announcements-repository-feature/fetch-details-of-a-binary-announcement-greeting-at-the-organization-level)
  - [Modify a binary announcement greeting](https://developer.webex.com/docs/api/v1/webex-calling-organization-settings-with-announcements-repository-feature/modify-a-binary-announcement-greeting)
  - [Fetch repository usage for announcements for an organization](https://developer.webex.com/docs/api/v1/webex-calling-organization-settings-with-announcements-repository-feature/fetch-repository-usage-for-announcements-for-an-organization)
  - [Fetch repository usage for announcements for an organization](https://developer.webex.com/docs/api/v1/webex-calling-organization-settings-with-announcements-repository-feature/fetch-repository-usage-for-announcements-for-an-organization)
  - [Delete an announcement greeting of an organization](https://developer.webex.com/docs/api/v1/webex-calling-organization-settings-with-announcements-repository-feature/delete-an-announcement-greeting-of-the-organization)

  The following APIs can upload and list announcements at the location level:

  - [Upload a binary announcement greeting at the location level](https://developer.webex.com/docs/api/v1/webex-calling-organization-settings-with-announcements-repository-feature/upload-a-binary-announcement-greeting-at-the-location-level),
  - [Fetch details of binary announcement greeting at location level](https://developer.webex.com/docs/api/v1/webex-calling-organization-settings-with-announcements-repository-feature/fetch-details-of-a-binary-announcement-greeting-at-location-level),
  - [Modify a binary announcement greeting](https://developer.webex.com/docs/api/v1/webex-calling-organization-settings-with-announcements-repository-feature/modify-a-binary-announcement-greeting),
  - [Fetch repository usage for announcements in a location](https://developer.webex.com/docs/api/v1/webex-calling-organization-settings-with-announcements-repository-feature/fetch-repository-usage-for-announcements-in-a-location)
  - [Delete an announcement greeting in a location](https://developer.webex.com/docs/api/v1/webex-calling-organization-settings-with-announcements-repository-feature/delete-an-announcement-greeting-in-a-location)

  The remaining APIs are modified to allow referencing the files in the announcement repository (updated with the `audioAnnouncementFiles` array):

  - [Create a call queue](https://developer.webex.com/docs/api/v1/webex-calling-organization-settings-with-announcements-repository-feature/create-a-call-queue)
  - [Get details for a call queue](https://developer.webex.com/docs/api/v1/webex-calling-organization-settings-with-announcements-repository-feature/get-details-for-a-call-queue)
  - [Update a call queue](https://developer.webex.com/docs/api/v1/webex-calling-organization-settings-with-announcements-repository-feature/update-a-call-queue)
  - [Read the list of call queue announcement files](https://developer.webex.com/docs/api/v1/webex-calling-organization-settings-with-announcements-repository-feature/read-the-list-of-call-queue-announcement-files)
  - [Get details for an auto attendant](https://developer.webex.com/docs/api/v1/webex-calling-organization-settings-with-announcements-repository-feature/get-details-for-an-auto-attendant)
  - [Create an auto attendant](https://developer.webex.com/docs/api/v1/webex-calling-organization-settings-with-announcements-repository-feature/create-an-auto-attendant)
  - [Update an auto attendant](https://developer.webex.com/docs/api/v1/webex-calling-organization-settings-with-announcements-repository-feature/update-an-auto-attendant)
  - [Get music on hold](https://developer.webex.com/docs/api/v1/webex-calling-organization-settings-with-announcements-repository-feature/get-music-on-hold)
  - [Update music on hold](https://developer.webex.com/docs/api/v1/webex-calling-organization-settings-with-announcements-repository-feature/update-music-on-hold)
  - [Get details for a call queue forced forward service](https://developer.webex.com/docs/api/v1/webex-calling-organization-settings-with-announcements-repository-feature/get-details-for-a-call-queue-forced-forward)
  - [Update a call queue forced forward service](https://developer.webex.com/docs/api/v1/webex-calling-organization-settings-with-announcements-repository-feature/update-a-call-queue-forced-forward-service)
  - [Get details for a call queue holiday service](https://developer.webex.com/docs/api/v1/webex-calling-organization-settings-with-announcements-repository-feature/get-details-for-a-call-queue-holiday-service)
  - [Update a call queue holiday service](https://developer.webex.com/docs/api/v1/webex-calling-organization-settings-with-announcements-repository-feature/update-a-call-queue-holiday-service)
  - [Get details for a call queue night service](https://developer.webex.com/docs/api/v1/webex-calling-organization-settings-with-announcements-repository-feature/get-details-for-a-call-queue-night-service)
  - [Update a call queue night service](https://developer.webex.com/docs/api/v1/webex-calling-organization-settings-with-announcements-repository-feature/update-a-call-queue-night-service)
  - [Get details for call queue stranded calls](https://developer.webex.com/docs/api/v1/webex-calling-organization-settings-with-announcements-repository-feature/get-details-for-a-call-queue-stranded-calls)
  - [Update a call queue stranded calls service](https://developer.webex.com/docs/api/v1/webex-calling-organization-settings-with-announcements-repository-feature/update-a-call-queue-stranded-calls-service)
