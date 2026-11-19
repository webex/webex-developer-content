---
type: Article
title: Webex People API Updates
canonical_url: https://developer.webex.com/blog/webex-people-api-updates
content_type: blog
date: '2022-09-15'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/webex-people-api-updates)

There are always new features coming to the Webex REST API; this update covers a few recent additions to the [People endpoint](https://developer.webex.com/docs/api/v1/people) used for interacting with Webex user data. Read along to get the full scoop on the new, extended, functionality.

### Add People Smarter

Now, Webex REST API accepts new fields to describe people. Here’s a full list of the added fields:

- PhoneNumbers
- Department
- Manager
- Title
- Country
- City

Support for these fields cannot be overstated, due to its role in making Webex People API a **powerful** tool for Admins to use for onboarding employees! All an `admin` needs to do is first disable Directory Connector to unlock this new potential. Any Webex user with the `admin` role (in production or a sandbox) can give this a try right away, or just read more information here: [Create a Person](https://developer.webex.com/docs/api/v1/people/create-a-person).

### Feature Subtraction: Data Security Edition

At one time, it was possible to use Webex People API to look up people across organizations using only an email address. Because this type of public directory had the potential to be exploited, it has been disabled. Also, an `id` is now required for user to `GET` a person’s details. This neutralizes any looming security threat, with the added possibility of less unwanted messages. However, users looking for messaging functionality specifically may continue to send `POST` requests with recipient’s email address to the `/messages` endpoint. Read about what it takes to `GET` personal details in our documentation here: [List People](https://developer.webex.com/docs/api/v1/people/list-people).

### Added Support for EVERYONE

Webex’s client applications allow users to set their preferred pronouns easily and choose whether to have them displayed to others. Soon, Webex REST API will return this information via a simple `GET` request to `/people/{personId}`. The value of inclusivity in the workplace is *priceless*! Coming in November, this feature must be enabled by an organization’s admin through [Control Hub](https://www.controlhub.webex.com/). Then, pronouns must be set using the Webex native client before People API can return them.

### Try It Yourself

Webex REST API’s range of dynamic features may inspire you to build an app of your own using the Webex Platform. To try out the features discussed in this blog, you’ll need a [Developer Sandbox](https://developer.webex.com/docs/developer-sandbox-guide) account. Then, you can try samples and learn all about Webex People API in our Developer Portal here: [People](https://developer.webex.com/docs/api/v1/people).

### TL;DR

Here’s a video summary of these updates to Webex REST API.

<iframe src="https://app.vidcast.io/share/embed/f4a96917-0bc5-47f5-b8c5-82d9e8efa643" width="100%" height="100%" title="Webex People API Updates" frameborder="0" loading="lazy" allowfullscreen style="position:absolute; top:0; left: 0"></iframe>

&nbsp;

### Keep Up with Us

**Stay in the loop with our social pages**

*Follow us on Twitter*

- [@WebexDevs](https://twitter.com/webexdevs)

*Watch Our Collection on Vidcast.io*

- [Webex Platform Developer Videos](https://app.vidcast.io/collections/share/97163a12-e567-413c-9eb6-bdcad681d4c3)

*Dive deeper*

- [developer.webex.com](https://developer.webex.com/)

*Join the conversation*

- [Webex for Developers Community Forum](https://community.cisco.com/t5/webex-for-developers/bd-p/disc-webex-developers)
