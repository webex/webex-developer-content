---
type: Article
title: Webex for Developers Newsletter – February 2024
canonical_url: https://developer.webex.com/blog/webex-for-developers-newsletter-february-2024
content_type: blog
date: '2024-02-26'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/webex-for-developers-newsletter-february-2024)

Greetings, Webex Developers! Since the beginning of the year, we have released several new updates that we want to share with you here. Let’s jump right to the details and get caught up on all the news.

### 📞Introducing the Webex Web Calling SDK

We are thrilled to unveil our new [Web Calling SDK](https://github.com/webex/webex-js-sdk/wiki/Introducing-the-Webex-Web-Calling-SDK), a robust toolkit designed for developers looking to integrate seamless Webex Calling features into their web applications. In a [new blog post](https://developer.webex.com/blog/introducing-the-webex-web-calling-sdk), Webex Engineering Leader, Sreekanth Narayanan, highlights all the key SDK features, benefits, and potential integration use cases of this SDK.

### 🤖Revolutionizing Incident Management in Webex with Command Bots

In a [white paper blog](https://developer.webex.com/blog/revolutionizing-incident-management-with-incident-command-bots) by Webex Developer Relations leader, Luz Delgado-Macias, discover how to optimize incident management with a custom-built Incident Command Bot. Also, learn more about the benefits of automation, power of customization, and unlimited potential for integrating with the Webex platform.

### ⚙️New Developer How-to Blogs

We recently published some helpful new developer blogs that show us how to work with *three* different types of Webex applications:

#### Webex Contact Center: Creating a Header Widgets in the Agent Desktop

In the first one, the leader of the Webex Developer Evangelism team, Adam Weeks, takes us through a step-by-step lab to [create an RSS Feed Reader in a Webex Contact Center Header Widget](https://developer.webex.com/blog/developing-with-webex-contact-center-header-widgets-an-rss-feed-reader-example).

#### Leveraging Service Apps for Secure and Scalable API Calls

Secondly, Webex Developer Evangelist, Joe Zanini, authored a guide to [create and manage Webex Service apps](https://developer.webex.com/blog/leveraging-service-apps-for-secure-and-scalable-api-calls-a-guide-for-admins-and-developers), to streamline authorizing org-level integrations for admins, and enabling efficient token consumption for developers to make API calls at scale.

#### Yarn Workspaces – Mono Repo and the Calling SDK

Finally, Webex Engineer, Kesava Krishnan Madavan, explains in detail how we can streamline the development process in the [Webex Calling SDK with Yarn Workspaces](https://developer.webex.com/blog/yarn-workspaces-mono-repo-and-the-calling-sdk). Kesava also shows us how these Yarn Workspace strategies can also be applied to various other Webex integration types.

### 📺Live Webinar: Intro to Webex Connect CPaaS APIs

On **Wednesday, February 28th at 1:00PM EST**, join us for the inaugural session of the [Webex Connect](https://cpaas.webex.com/) webinar series and explore the potential of CPaaS. This session offers a comprehensive introduction to the platform, showcasing the APIs, developer tools and building blocks you can use to integrate powerful communications capabilities into your applications and accelerate customer experience transformation. Learn from a live demonstration how to quickly create and launch customer journeys leveraging serverless computing and AI in a secure and scalable environment. [Register](https://evangelism.webex.com/weblink/register/racd916f80e2689acfa2110e7f4f5bd63) to attend the live webinar or watch the recording after on the [Developer Webinars page](https://developer.webex.com/webinars).

### 🧑‍💻New Developer Guides for Webex Wholesale &amp; Webex for BroadWorks APIs

We also just released refreshed developer guides pertaining to [Webex Wholesale](https://help.webex.com/en-us/article/nkguodc/Wholesale-Route-to-Market-Solution-Guide) and [Webex for BroadWorks](https://help.webex.com/en-us/article/no4dlj3/Webex-for-Cisco-BroadWorks-Solution-Guide) APIs:

[Webex for Wholesale Developer Guide](https://developer.webex.com/docs/wholesale)**:** Learn how to leverage the Webex for Wholesale Provisioning APIs, for allowing Partners to use the Webex Suite as a Package based Utility Model.

[Webex for BroadWorks Developer Guide](https://developer.webex.com/docs/webex-for-broadworks-developers-guide): Learn how Service Providers can leverage the Webex for BroadWorks Provisioning APIs, to automatically onboard, update, and remove Webex services for their subscribers.

### 🦾Embracing the Power of AI at Cisco Live Amsterdam

In a [post-event wrap up](https://blog.webex.com/hybrid-work/webex-integration-partners-cisco-live-amsterdam/?utm_medium=Organic_Social&amp;utm_source=LinkedIn&amp;team=Social), Business Development Manager, Colm Mcnelis highlights the latest technology innovations that were showcased by our Webex partners, with a special focus on driving digital transformation using the power of AI.

### 🌅Retiring the Legacy Webex Meetings XML APIs

The [Meetings-related XML APIs](https://developer.cisco.com/docs/webex-xml-api-reference-guide/#!meetings-xml-api-reference-guide/webex-meetings-xml-api-reference-guide) have been deprecated and the End-of-Support (EoS) date is planned for the second half of 2023. Cisco will continue to resolve bugs up to this date, but new features will only be implemented for the REST APIs suite. The End-of-life (EoL) timeframe for Meetings-related XML APIs is targeted for **March 31, 2024**, at which time they will be retired. For information on how to migrate from XML to REST APIs, please see the [Webex Meetings XML to REST Migration Guide](https://developer.cisco.com/docs/webex-xml-api-reference-guide/#!meetings-xml-api-reference-guide/webex-meetings-xml-api-reference-guide).

### 📝Webex API Changelog Highlights

The [Webex API Changelog](https://developer.webex.com/docs/api/changelog) has several recent entries listed. We always recommend checking that page frequently to stay up to date. Here are some important entries to note:

- **February 7, 2024 - BREAKING CHANGE:** If a BroadWorks Subscriber exists but contains errors, the [Get a BroadWorks Subscriber](https://developer.webex.com/docs/api/v1/broadworks-subscribers/get-a-broadworks-subscriber) and [List BroadWorks Subscribers](https://developer.webex.com/docs/api/v1/broadworks-subscribers/list-broadworks-subscribers) APIs now return the `errorCode` as integer in the errors array.
- **January 31, 2024 - NEW:** We are proud to announce the availability of the new [guest creation mechanism](https://developer.webex.com/docs/api/v1/guests-management) via Service Apps. Guests are now created from authorized Service Apps with guest-issuer scopes
- **January 25, 2024 - NEW**: In the [Virtual Line Call Settings](https://developer.webex.com/docs/api/v1/virtual-line-call-settings) API, we've added multiple endpoints that let you create and manage Virtual Lines and subsets of their call settings.
