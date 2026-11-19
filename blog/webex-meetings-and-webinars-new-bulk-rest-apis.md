---
type: Article
title: 'Webex Meetings and Webinars: New Bulk REST APIs'
canonical_url: https://developer.webex.com/blog/webex-meetings-and-webinars-new-bulk-rest-apis
content_type: blog
date: '2022-08-01'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/webex-meetings-and-webinars-new-bulk-rest-apis)

As more enterprises adopt better strategies for hybrid work, integrations for Webex [Meetings](https://developer.webex.com/docs/meetings) and [Webinars](https://developer.webex.com/docs/webinar-guide) need to continually scale higher and higher. Many deployed Webex meeting integrations automate scheduling and management of events for thousands of users at any given time. This uptick in usage results in apps making increasingly more API calls to the Webex platform. With some webinars having up to 10,000 participants, Webex integration developers want to ensure they are utilizing the APIs efficiently and keep queries to a minimum. We are pleased to announce some new Meetings REST API endpoints that will help to significantly reduce the amount of API calls previously needed for managing registration lists and other bulk tasks. Let’s explore these new methods.

### Bulk Registration for Webex Meetings and Webinars

One of the most notable bulk API updates is the new endpoint to [Batch Register Meeting Registrants](https://developer.webex.com/docs/api/v1/meetings/batch-register-meeting-registrants). Previously, when applications utilized Webex Meetings APIs to automate registrations for a Meeting or a Webinar, a separate API was needed for each individual participant to be registered. This new API allows bulk registration of participants, where an array of participant emails can be sent in a single API call to batch register them for a specific meeting or webinar. It’s easy to see how this can drastically lower the amount of API usage, particularly with integrations that manage large webinars.

### Query the List of Registrants and Participants

We also brought some new functionality to the REST APIs that was formerly exclusive to the [Webex XML APIs](https://developer.webex.com/docs/webex-xml-api-deprecation-announcement). First, a host and cohost of a meeting/webinar can now make API call that includes an email or array of emails to retrieve registrant details, through a new API - [Query Meeting Registrants](https://developer.webex.com/docs/api/v1/meetings/query-meeting-registrants). This request can also be further refined to query by the status of a registrant - `approved`, `pending`, or `rejected`. When the status for a group of registrants needs to be updated, it can now also be accomplished in a single API call through the new endpoint [Batch Update Meeting Registrants Status](https://developer.webex.com/docs/api/v1/meetings/batch-update-meeting-registrants-status). Lastly, there’s another similar new API that enables integrations to [Query Participants by Email Address](https://developer.webex.com/docs/api/v1/meeting-participants/query-meeting-participants-with-email), either during a live meeting or after it ends. Again, Webex integrations that work with large audiences can now be more flexible and efficient.

### Filter List of Meetings by Type (meeting or webinar)

To make lists meetings and webinars more manageable for integrations, the [Webex list meetings API](https://developer.webex.com/docs/api/v1/meetings/list-meetings) has been updated to allow applications to list meetings by either `meeting` or `webinar`, via the new parameter `meetingType`. This filter allows developers to work with more specific data in their integrations and reduce the amount and unwanted results when retrieving meeting lists.

### Need Some Help? We Got You Covered!

We are excited to provide you with these new bulk APIs that should reduce the volume of API calls needed to work with Webex Meetings and Webinars. If you need help, the&#xa0;[Webex Developer Support Team](https://developer.webex.com/support)&#xa0;is standing by and happy to assist. You can also start or join a conversation on the Webex for [Developers Community Forum](https://cs.co/WebexDeveloperCommunity) or tweet us&#xa0;[@WebexDevs](https://twitter.com/WebexDevs) with your comments and requests. In the meantime, have fun with the new updates and happy developing!
