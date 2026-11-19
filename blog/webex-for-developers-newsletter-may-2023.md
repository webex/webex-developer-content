---
type: Article
title: Webex for Developers Newsletter – May 2023
canonical_url: https://developer.webex.com/blog/webex-for-developers-newsletter-may-2023
content_type: blog
date: '2023-05-30'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/webex-for-developers-newsletter-may-2023)

Hello again, Webex Developers! As usual, we’ve gathered a lot of great updates, announcements, and other interesting tidbits in this month’s newsletter. So, let's jump right in and check out the latest stories.

### 🎤 Webex for Developers Sessions at Cisco Live - Las Vegas

Viva Las Vegas! Come join the Webex for Developers team at Cisco Live in Las Vegas on June 4 - 8, 2023. There are a lot of great classroom and workshop sessions scheduled inside the DevNet Zone that you won’t want to miss. Manager of the Webex Dev Evangelism team, Adam Weeks, provides the full rundown in a [new blog post](https://developer.webex.com/blog/webex-for-developers-at-cisco-live-vegas-2023).

### ✨ Getting to Know Webex OAuth Integrations

Thanks to the extensive collection of APIs, it’s possible for [integrations](https://developer.webex.com/docs/integrations) to do powerful things inside of Webex and they need to be secure. This is why Webex integrations use OAuth 2.0 standard for generating API access tokens. We have two new developer blog posts related to several aspects of an OAuth grant flow for integrations. In the first one, Software Engineer, Sandip Banerjee, shows us the methods for [obtaining an access and refresh token](https://developer.webex.com/blog/generating-an-oauth-token-pair-using-a-webex-integration) for any Webex integration.
Additionally, you can also discover about the importance of picking the right scopes for Webex Calling Integrations in [another blog post](https://developer.webex.com/blog/picking-the-right-scopes-with-webex-calling-oauth-integrations) by Adam Weeks.

### 📇 Webex Contact Center APIs and Dev Portal

In a [recent blog post](https://developer.webex.com/blog/introducing-the-webex-contact-center-apis-and-developer-portal) by Software Engineering Leader, Arunabh Bhattacharjee, you can learn how the Webex Contact Center APIs surfaces the power of the platform and makes them available publicly to integration developers on the updated Contact Center for Developers portal.

### 🥼 Webex for Developers Beta Program

We are excited to announce that the Webex Developer Beta program is officially OPEN! With the support of the [Webex Beta Platform](https://www.essentials.webex.com/programs/webex-beta), you now have the opportunity to access the Webex Developer Platform's APIs, SDKs, and other features before anyone else. By joining today, you will have access to our latest feature, the API for space linking to Enterprise Content Management folders, which you can evaluate upon registration. [Register now](https://gobeta.webex.com/key/dev-platform) to take advantage of this exclusive program.

### 🎥 Accessing Real-time Webex Meeting Media

Check out the [new guest column](https://developer.webex.com/blog/how-to-build-meeting-bots-for-webex) by Webex development partner, Recall.ai, where they describe how they make their own kind of meeting-bot, by combining guest issuer and the Webex Browser SDK to enable media access to an integration.

### 📊 New! Webex Status APIs

In another great update ,you can now access our [status page](http://status.webex.com/) via API. Stay updated on any service disruptions or maintenance and keep your communication running smoothly. Software Engineer, Sandip Banerjee, explains it all in a [new blog post](https://developer.webex.com/blog/how-to-build-meeting-bots-for-webex).

### 🃏 Webex Buttons &amp; Cards Enhanced Performance

Webex messaging [buttons &amp; cards](https://developer.webex.com/docs/buttons-and-cards) are now even better! In [another great article](https://developer.webex.com/blog/buttons-and-cards-spaces-are-5-times-faster-to-load-with-50-less-memory-footprint), Software Engineering Technical Leader, Hem Dutt, shows us how Webex Spaces with Buttons &amp; Cards are now 5X Faster to Load with 50% Less Memory Footprint, resulting in a noticeably improved end-user experience.

### 🧑‍🔧 Developer Support is Seeking Your Input

The [Webex Developer Support](https://developer.webex.com/support) team is committed to providing fast and accurate answers to your questions and help you overcome any challenges. To better serve the needs of the extensive number of users on our platform, we’ve recently transitioned from a messaging space (Webex4Dev) support model to a community forum-based model.

We’re eager to hear from you about this change - please take a quick minute to respond to [this short survey.](https://www.surveymonkey.com/r/LXS7FNW)

### 🪵 Webex API Changelog Highlights

The [Webex API Changelog](https://developer.webex.com/docs/api/changelog) has some more recent entries, so continue to keep a close on eye on it. Here are a couple important ones to note for this month:

- **May 10, 2023 – WARNING:** As a Compliance Officer, you are always allowed to retrieve `temporaryDirectDownloadLinks` using the [Get Recording Details API](https://developer.webex.com/docs/api/v1/recordings/get-recording-details), even if the recording is flagged to prevent downloads.
- **May 15, 2023 – NEW**: Orgs that have tracking codes enabled and an admin has mapped a tracking code to custom (or user profile attributes,) they cannot [create a tracking code](https://developer.webex.com/docs/api/v1/tracking-codes/create-a-tracking-code), [update a tracking code](https://developer.webex.com/docs/api/v1/tracking-codes/update-a-tracking-code), [delete a tracking code](https://developer.webex.com/docs/api/v1/tracking-codes/delete-a-tracking-code), or [update user tracking codes](https://developer.webex.com/docs/api/v1/tracking-codes/delete-a-tracking-code). Admins can [list mapped tracking codes](https://developer.webex.com/docs/api/v1/tracking-codes/list-tracking-codes), [get a mapped tracking code](https://developer.webex.com/docs/api/v1/tracking-codes/get-a-tracking-code), and [get user mapped tracking code](https://developer.webex.com/docs/api/v1/tracking-codes/get-user-tracking-codes) when the mapping process has completed. Learn more [here](https://help.webex.com/en-us/article/preview/nxrfr9v/User-attributes-in-Control-Hub#task-template_39f4e0fd-e1fd-459c-9e2a-93b07251b3a9).
