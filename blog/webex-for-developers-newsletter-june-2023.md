---
type: Article
title: Webex for Developers Newsletter – June 2023
canonical_url: https://developer.webex.com/blog/webex-for-developers-newsletter-june-2023
content_type: blog
date: '2023-06-27'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/webex-for-developers-newsletter-june-2023)

### 🎤Webex for Developers at Cisco Live 2023 - Las Vegas

The Webex for Developers community made their presence known in a big way at Cisco Live in Las Vegas. There were classroom sessions, hands-on workshops, and a fantastic full-day Webex takeover inside the DevNet Zone that featured some amazing integration partners. The manager of the Webex Dev Evangelism team, Adam Weeks, provides the full wrap up in a [new blog post](https://developer.webex.com/blog/cisco-live-us-2023-unleashing-the-power-of-webex-developers).
Additionally, for an in-depth look at even more Webex integrations partners that were showcased at Cisco Live to advance hybrid workflows, check out [this blog post](https://blog.webex.com/hybrid-work/webex-integration-partners-at-cisco-live-las-vegas/) by Business Development Manager, Colm Mcnelis.
And finally, in [another blog post](https://blog.webex.com/cloud-calling/webex-calling-at-cisco-live-2023/), Product Marketing Leader, Manu Parhar, explains all the unrivaled Webex Calling experiences that were introduced at Cisco Live.

### ✨Introducing Webex Sidebar Apps

We are excited to announce that developers can now build Sidebar Apps inside of Webex, which are a new type of Embedded App that exists outside of Meetings or Messaging Spaces. Sidebar Apps can satisfy a variety of use cases, such as AI virtual assistants, CRM lookups, company directory, employee wellness, and more! Developers can also configure these applications to run continuously, so that when you launch the Webex, the Sidebar apps will run in the background automatically. Senior Product Manager, Omar Elrafei, explains it all [here](https://developer.webex.com/blog/webex-sidebar-apps).

### 🖥️New! Presentation Mode for Embedded Apps

Omar Elrafei also recently announced another new feature enhancement to the Webex Embedded Apps Framework - Presentation Mode. This allows developers to screen share their app directly from within Webex, which is exclusively controlled by a single user in a meeting. This is useful in industry verticals such as education and healthcare where, in some cases, the content of the app is not meant for collaborative use. Get the full details [here](https://developer.webex.com/blog/seamlessly-share-your-apps-in-webex).

### 🔐Real-world walkthrough of OAuth Integrations

Properly implementing an OAuth grant flow for Webex integrations is always a hot topic amongst our developer community. Integrations are how you request permission to invoke the Webex REST API on behalf of another Webex user. To do this in a secure way, the Webex APIs support the&#xa0;[OAuth 2](http://oauth.net/2/) standard which allows third-party integrations to get a temporary access token for authenticating API calls. In a refreshed [how-to blog post](https://developer.webex.com/blog/real-world-walkthrough-of-building-an-oauth-webex-integration), Developer Evangelist, Joe Zanini, goes into a deep dive explanation of OAuth 2, what it is used for, and how to manage it in Webex integrations using Python and Flask.

### 📱Webex and AT&amp;T Join Forces

Webex and AT&amp;T are teaming up to deliver the next evolution in mobility solutions for those working on the go. This partnership extends Webex Calling capabilities to AT&amp;T supplied data plans and mobile phones via a single business phone number that becomes your identity for all your Webex Communications. Users will have access to powerful calling features natively from their mobile dialer. SVP/GM of Cisco Collaboration, Lorissa Horton, tells us all about it [here](https://blog.webex.com/cloud-calling/webex-and-att-unrivaled-mobility/).

### 🤖Try Out These New Bots in the App Hub

There are a couple of new bots on the [Webex App Hub](https://apphub.webex.com/) that are built by Cisco and powered by the [Messaging APIs](https://developer.webex.com/docs/messaging) &amp; [Buttons &amp; Cards](https://developer.webex.com/docs/buttons-and-cards) feature, to help enhance user productivity in Webex:

- [Google Form Bot for Webex](https://apphub.webex.com/applications/google-form-cisco-systems) - Receive notifications for Google form submissions inside any Webex space.
- [Dropbox Sign Bot for Webex](https://apphub.webex.com/applications/dropbox-sign-cisco-systems) - Receive document e-signature action notifications in any of your Webex spaces.

<br/>

### 🪵Webex API Changelog Highlights

The [Webex API Changelog](https://developer.webex.com/docs/api/changelog) has more recent entries, so continue to keep a close on eye on it. Here are a couple important ones to note for this month:

- **June 20, 2023 – NEW:** The Meetings API now supports the following options: requiring attendees to sign in before joining a webinar and restricting the webinar to invited attendees only. The following endpoints now support the parameters `requireAttendeeLogin` and `restrictToInvitees`: [Create a Meeting](https://developer.webex.com/docs/api/v1/meetings/create-a-meeting), [Get a Meeting](https://developer.webex.com/docs/api/v1/meetings/get-a-meeting), [List Meetings](https://developer.webex.com/docs/api/v1/meetings/list-meetings), and [Get a Meeting Template](https://developer.webex.com/docs/api/v1/meetings/get-a-meeting-template).
- **June 20, 2023 – Breaking Change**: Webex Calling APIs we will not return fields with `null` values any longer to be consistent with the rest of our API set. Fields that have a `null` value will be omitted from the response. This change will be enforced on August 1, 2023.
