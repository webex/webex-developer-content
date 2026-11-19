---
type: Article
title: Webex for Developers Newsletter – December 2023
canonical_url: https://developer.webex.com/blog/webex-for-developers-newsletter-december-2023
content_type: blog
date: '2023-12-18'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/webex-for-developers-newsletter-december-2023)

Greetings, Webex Developers! We again have a lot of new items to share this month, particularly on the Webex Contact Center platform. Let’s get right to the news and see what’s going on!

### 🧑🏾‍💻Custom Widgets in the Webex Contact Center Agent Desktop

We have been really ramping-up our developer content for Webex Contact Center over the past month, starting with building custom widgets in the Agent Desktop.

First, Developer Evangelist, Joe Zanini, published a [new blog post](https://developer.webex.com/blog/unlocking-the-power-of-custom-widgets-in-webex-contact-center), where he explores how custom widgets can transform customer interactions, improve agent productivity, and deliver exceptional customer service experiences.

Next, check out the [webinars page](https://developer.webex.com/webinars) to watch the recording of last month’s live session, where Developer Evangelism leader, Adam Weeks, delved into widget development for Webex Contact Center, key customization areas, widget types, and how developers can start building today.

### 🔦Are You New to Webex Contact Center for Developers? No Problem!

When you are ready to start exploring development on the [Webex Contact Center platform](https://developer.webex.com/webex-contact-center/docs), we recently published some helpful Vidcasts to help you get started:

1. In the [first Vidcast](https://app.vidcast.io/share/25cc9f50-fc9b-4d86-8dda-0527ad911073), take a tour of the Webex Contact Center for Developers portal for a quick primer on navigating the site and to learn what resources are available to for building integrations, desktop widgets, and much more.
1. In the [next recording](https://app.vidcast.io/share/057f07a2-87ab-4288-96f3-c5e42dee9263), find out the process for requesting a Webex Contact Center developer sandbox and the requirements for doing so.
1. Once your sandbox request is approved, you can learn all the specifics on getting it provisioned and configured for testing in [this Vidcast](https://app.vidcast.io/share/396869f8-726e-43b8-8a10-b99016c781c3).

<br/>

### 📃Discover the Webex Contact Center for Developers Changelog Page

If you read previous editions of this newsletter, you probably know that we provide a link to the Webex Developer platform changelog in the bottom section. However, did you know that the Contact Center APIs have their own [changelog page](https://developer.webex.com/webex-contact-center/docs/api/changelog/webex-contact-center)? Be sure to also check in there frequently for the most up to date listings.

Some notable Contact Center API changelog entries that were recently listed:

- **November 15, 2023 - NEW:** A new API has been added to the Contact Service Queue Resource. Retrieving a list of contact service queues is now supported via the [List Contact Service Queues API](https://developer.webex.com/webex-contact-center/docs/api/v1/contact-service-queues/list-contact-service-queues). Also note that Get Contact Service Queue V2 API response doesn’t contain `callDistributionGroups` information. In order to fetch the `callDistributionGroups`, use the [Get a Contact Service Queue By ID API](https://developer.webex.com/webex-contact-center/docs/api/v1/contact-service-queues/get-specific-contact-service-queue-by-id).
- **November 15, 2023 - DEPRECATIONS:** The following APIs have updated endpoints:
  - The [List Contact Service Queue v1 API](https://developer.webex.com/webex-contact-center/docs/api/v1/contact-service-queues/list-contact-service-queues) will be deprecated on Jan. 13, 2024. [The List Contact Service Queues v2 API](https://developer.webex.com/webex-contact-center/docs/api/v1/contact-service-queues/list-contact-service-queues) should be used instead.
  - The [List Skill Profile v1 API](https://developer.webex.com/webex-contact-center/docs/api/v1/skill-profile/list-skill-profiles) will be deprecated on Jan. 13, 2024. The [List Skill Profiles v2 API](https://developer.webex.com/webex-contact-center/docs/api/v1/skill-profile/list-skill-profiles) should be used instead.
  - The [List Outdial ANIs v1 API](https://developer.webex.com/webex-contact-center/docs/api/v1/outdial-ani/list-outdial-anis) will be deprecated on Jan. 13, 2024. The [List Outdial ANIs v2 API](https://developer.webex.com/webex-contact-center/docs/api/v1/outdial-ani/list-outdial-anis) should be used instead.

<br/>

### 🎊Live Webinar: Webex Developer Year-in-Review

There has been a lot of additions to the Webex platform in 2023, giving developers more tools and resources to build powerful integrations. In the next webinar scheduled on December 20th at 1:00PM EST, join us for a roundup of the most notable Webex platform updates and other developer news items from the past year. The live session includes an attendee drawing for a cool prize! 

You won’t want to miss this one – head over to our [webinars page](https://developer.webex.com/webinars) to check it out.

### 📝Webex API Changelog Highlights

The [Webex API Changelog](https://developer.webex.com/docs/api/changelog) has several recent entries listed. We always recommend checking that page frequently to stay up to date. Here are some important entries to note:

- **November 30, 2023 - NEW:** The Service Apps with meetings functionalities as indicated by `meetings:*` scopes can now be tied to specific sites in the organization. This selection is done by a full admin in Control Hub who authorizes the Service App for the required site(s). The admin can choose from any or all of the meetings sites in the organization. The service app can only act on the allowed sites. As an example let's assume an organization with two sites A and B. An admin wants to use a meeting scheduling Service App, but wants to allow this Service App only for site A. The admin would during the authorization process select site A and the Service App will not be able to schedule meetings on site B.

- **December 6, 2023 - NEW:** The API, [Activate phone numbers in a location](https://developer.webex.com/docs/api/v1/numbers/activate-phone-numbers-in-a-location), supports a maximum of 500 phone numbers.
- **December 6, 2023 - BREAKING CHANGE:** The APIs [Add Phone Numbers to a location](https://developer.webex.com/docs/api/v1/numbers/add-phone-numbers-to-a-location), [Activate Phone Numbers in a location](https://developer.webex.com/docs/api/v1/numbers/activate-phone-numbers-in-a-location), and [Remove phone numbers from a location](https://developer.webex.com/docs/api/v1/numbers/remove-phone-numbers-from-a-location) now require phone numbers in the E.164 format for all countries.
