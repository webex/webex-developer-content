---
type: Article
title: Webex Meetings API Updates
canonical_url: https://developer.webex.com/blog/webex-meetings-api-updates
content_type: blog
date: '2022-11-30'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/webex-meetings-api-updates)

Wow, the closing of 2022 is upon us! As we charge into 2023, we're riding on a wave of new features across the Webex Developer Platform. Here's some good news from the world of the Webex Meetings REST APIs. But first, let's take a peek at what you can do with the Webex Meetings APIs in general. 

With the Meetings API, you can do things like:

- Create and manage meetings
- Add and manage meeting invitees
- Get and update meeting preferences, options, and other details
- Get, list, and delete recordings

Let's take a look at some of the _new_ features the API now offers: Webex Organization Administrators now have the ability to [retrieve meeting recordings of all users of a Webex site via the Meetings API](https://developer.webex.com/docs/meetings#adminorganization-level-authentication-and-scopes). This allows admins and compliance systems easy access to all user's recordings.  This is commonly used in data mining or custom archiving solutions for efficient recording retrieval.

The Webex REST API has added support for [pulling recordings from multiple Webex sites](https://developer.webex.com/docs/api/v1/recordings/list-recordings). Large enterprises often have several sites provisioned, and employees have access to host meetings on any of these. For example, here at Cisco we have half a dozen sites. Two of those are dedicated to beta features. We work with customers that use sites to segment their business purposes. One customer does all their board meetings on a special site. Since employees can schedule meetings on several sites, depending on the business need, the recordings may be equally distributed over these sites. With this new feature, a host's recordings can be accessed from all the sites they had meetings.

The [meetings recordings recycle bin](https://developer.webex.com/docs/api/v1/recordings/move-recordings-into-the-recycle-bin) has added API support. Today, in the webex GUI (`https://sitename.webex.com`) the recording owner can move a recording to the recycle bin, restore from the recycle bin, and empty the recycle bin. We have exposed this feature in the API as well. You can move recordings to the recycle bin, restore them, and purge them. Compliance Officers can do the same with recordings belonging to their org's users, especially where undesirable recordings need to urgently be deleted.

[List meeting recordings can now show deleted recordings](https://developer.webex.com/docs/api/v1/recordings/list-recordings). A `status==deleted` indicates that the recording is permanently deleted. This way a user with malicious recordings has no way to completely hide their wrong doing. A tombstone of the recording will always be available.

[Post Event Survey results can be accessed via the REST API](https://help.webex.com/en-us/article/nbet0py/Create-a-Post-Event-Survey-and-Add-it-to-an-Event). Post Event Surveys contain a plentitude of meaningful data, used by businesses to improve their offerings, workflows, or simply to understand which webinars are best suited to an audience. As such, machine based data mining of the Event Surveys is crucial to being able to improve the offer and processes. With this API we achieve post event data access in the REST API. This also makes it easier for current XML API users to migrate these workflows.

Here's a feature you'll need to request if you want it on your org: Q&A and Polling Data from meetings are available through the Webex REST API via the `/events` endpoint for archival at the third party provider of the customer's choice. Especially if you operate in a sensitive vertical or are subject to *Finra2010* requirements you are encouraged to make use of this API.

We're also now supporting [Source IDs in Webinars](https://help.webex.com/en-us/article/nzgyjep/Track-Your-Cisco-Webex-Events-Attendees), allowing you to track the source of traffic to your events identifying your most successful channels and partners and rewarding them for their good work 😊 . Source IDs complement the ability to set and retrieve tracking codes which are available now, too.

### Further Reading

The Webex REST APIs cover much more than just Meetings. Looking for a good place to get started? <https://developer.webex.com/docs/getting-started> has you covered!

Please don't hesitate to reach out on the Webex Developer Community Forum if you want to discuss the Webex Developer Platform with us, and we hope you have a happy holiday season!
