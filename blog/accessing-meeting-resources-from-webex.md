---
type: Article
title: Accessing Meeting Resources from Webex
canonical_url: https://developer.webex.com/blog/accessing-meeting-resources-from-webex
content_type: blog
date: '2021-07-12'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/accessing-meeting-resources-from-webex)

### Accessing Meeting Resources from Webex
Web Developers have requested an improved capability to access and connect to the resources that allow their applications to get direct access to post meeting resources for proper analysis. They need to know what meetings are occurring, who the participants in each individual meeting, when these meetings start and end and how to access the content from these meetings.

#### New Features
There are two new features that can meet this need.

 - Recording: To record the meeting, you must enable the recordings option. This can be done by the users during a meeting or programmatically via API for a scheduled meeting.
 - Transcripts: To create a transcript, you must turn on Webex Assistant. This cannot be done programmatically and must be turned on by the meeting host/participant or set as default behavior in the control hub. NOTE: Webex Assistant requires a license.

After a meeting has finished, Webex will process and store post meeting assets and make them available through the endpoint. You can query for all available recordings by leaving the query parameters blank or you can set specific data. These meeting assets are designed for closed captioning applications and not for parsable machine applications. The txt format does include speaker name but is not delimited in a way that lends itself to being parsed programmatically.

Possible Benefits and Uses of This Technology
This will provide third party developers access meeting resources that will allow them to review sales calls, find out who was present, and then create a new tactical sales strategy in their never-ending quest to find new business partners. New sales AI platforms can review the transcripts use them to determine intent and which potential partners are worth chasing while measuring real world metrics in the meeting.

Those in the Compliance Offer role will be able to example transcripts to ensure that nothing improper happened at a meet and that no one was there that shouldn’t have been to ensure that trade secrets are kept and that all compliance regulations are met.

#### Closing
You can the Accessing Meeting Resources guide [here][1].


  [1]: https://developer.webex.com/docs/access-meeting-resources-guide
