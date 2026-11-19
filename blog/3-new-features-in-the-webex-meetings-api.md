---
type: Article
title: 3 NEW Features in the Webex Meetings API
canonical_url: https://developer.webex.com/blog/3-new-features-in-the-webex-meetings-api
content_type: blog
date: '2022-08-24'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/3-new-features-in-the-webex-meetings-api)

The Webex Meetings API added some **powerful** features recently. Here’s a brief overview to bring you up to date on the latest Meetings API developments.

### Closed Captioning Provided by Webex

Several of our close partners have requested it, and here it is: Closed captions, also called meeting transcripts, are now retrievable from Webex Meetings API without needing to record the meeting itself! This feature is incredibly important for businesses who conduct customer-facing Webex Meetings. Compliance officers at these companies can now access un-enhanced meeting transcript data complete with speaker, datetime, and meeting metadata and export it to a 3<sup>rd</sup>-party processor for archival. For usage details, head over to our documentation [here](https://developer.webex.com/docs/api/v1/meeting-closed-captions).

### Break-Out Sessions now RESTful

Webex REST API now supports full “CRUD” operations for break-out sessions. This means you can enable break-out sessions in a meeting and configure them when creating a meeting, read or update their info, and delete them. It’s also possible to create meeting templates that include enabled break-out sessions and their configuration. This feature was previously available through our, soon to be deprecated, [Webex XML API](https://developer.webex.com/docs/webex-xml-api-deprecation-announcement). Follow this [link](https://developer.webex.com/docs/api/v1/meetings) to the docs covering the `/meetings` endpoint to find the updated breakout sessions specifications. The `Create`, `Read`, and `Update a Meeting` methods have descriptions of the `enabledBreakoutSessions` and `breakoutSessions` properties that you’ll need to implement this. You can also read about how to [Update](https://developer.webex.com/docs/api/v1/meetings/update-meeting-breakout-sessions), `Read`, and `Delete` breakout sessions according to their `meetingId` via a new nested endpoint:

```none
https://webexapis.com/v1/meetings/{meetingId}/breakoutSession
```

### Meetings: Gotta Get ‘em ALL

Administrators may need the option to retrieve all a user’s meeting data, but if the user-in-question belongs to an organization with more than one Webex site, said administrator would need to provide our API a `siteURL` value. With this recent update, leaving this option blank will return a paginated list of the user’s meetings on ALL their “sites”. To learn how to implement this yourself, read our documentation on the subject [here](https://developer.webex.com/docs/api/v1/meetings/list-meetings).

### Pause, Rewind…

**TL:DR?** Here I am, filling you in about these features in a brief video you can watch on-the-go.


  <iframe src="https://app.vidcast.io/share/embed/3d03d205-30cc-4750-bc27-bad76a88ce93" width="100%" height="100%" title="Webex Meetings API Updates" frameborder="0" loading="lazy" allowfullscreen style="position:absolute; top:0; left: 0"></iframe>


&nbsp;

### Follow Along

Don’t miss any Webex news! Product announcements, feature updates, and more are at your fingertips when you join our [Webex Developer Community](http://cs.co/webexdevelopercommunity) and follow our Twitter [@WebexDevs](https://www.twitter.com/webexdevs).
