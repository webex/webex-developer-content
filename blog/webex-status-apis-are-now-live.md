---
type: Article
title: Webex Status APIs Are Now Live
canonical_url: https://developer.webex.com/blog/webex-status-apis-are-now-live
content_type: blog
date: '2023-05-04'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/webex-status-apis-are-now-live)

Before planning a large webinar, before importing a chunk of new accounts in Control Hub, or even during the preparation of an automated application using Webex APIs at a large scale, it plays a pivotal role to make sure these Webex services are up and running. Previously, if you needed to check the status of Webex and its services, you would visit <https://status.webex.com> and go through the dashboard as shown below. Unfortunately, there was no way to programmatically access the information.

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt13640e512676dd29/6452b1a8dd503e10d95b8100/webex-status-apis-are-now-live-2.png)

The wait is finally over! We would like to introduce the Webex Status APIs here for various Webex Services, which are now live. We can now validate the status of every Webex service with a simple API call and access current as well as historical data programmatically.

### Overview of the Webex Status APIs

The following are the Webex Status APIs currently available in our system:

- Summary
- Status
- Components
- Incidents
  - Unresolved incidents
  - All incidents
- Scheduled maintenance
  - Upcoming scheduled maintenance
  - Active scheduled maintenance
  - All scheduled maintenance

<br/>

### Understanding a couple of Status APIs and what those deliver

Since now we know the classification of Status APIs, we wanted to portray some of the APIs here and share a brief introduction to those.

#### All Incidents API endpoint

<https://status.webex.com/all-incidents.json>

As the name suggests, this API Response includes the current unresolved incidents of different Webex Services as well as the incidents that have already been resolved. The response should have the unique incident ID, incident name and most importantly, the incident’s status. Every incident’s *created_date* and *updated_date* should provide a clear picture of the continuous progress of the incident. When the incident has been resolved, the *resolved_at* should be present. Along with that, to understand which incident is impacting which Webex service area, the *product_group* field should help there and possible values for the *product_group* field should be “WebexTeams” (Webex Messaging), “WebexMeetings”, “WebexContactCenter”, etc.

#### Components API Endpoint

<https://status.webex.com/components.json>

It might create some confusion when we look at the Summary API endpoint and try to compare the result with the Component API since they might look almost similar. However, the Component API endpoint result gets into a more granular level than the Summary API endpoint.
To discuss the difference in detail, the Summary API accumulates the different *product_groups*, shares the information of their overall availability with the help of the *status* field, and provides the different component IDs that fall under those *product_groups*, though it doesn’t share the status of each component.
That is where the role of the Components API comes into play, which gets into more detail and shares the status of each component ID along with the component name under those *product_groups*.
From the Summary API response, we can copy the component ID under a specific *product_group* and search for the corresponding details of that component ID under the Components API response.

### Overall Webex Status API definitions

To understand the behavior of each Webex Status API, please go through [this](https://developer.webex.com/docs/webex-status-api) Webex Developer Portal page. This page contains a brief description of each Status API and holds the redirect links to their sample response properties as well.

### Postman collection for the Webex Status API

Now that we understand the different Status APIs that are currently available and that it also depicts which set of tasks can be done through these APIs, we still believe a complete Postman collection with the exact API details would be helpful to get the real job done. 
So, here it is! Kindly go through the GitHub page - [https://github.com/WebexSamples/WebexStatusAPI](https://github.com/WebexSamples/WebexStatusAPI).

Simply clone this repo to your personal system, and once it’s done, import the file `status-api-postman-collection.json` in Postman, and that will directly create the collection of the Status API under your Postman account.

Steps to import the file in Postman and a sample API request are shared over the provided GitHub [docs/ImportAndConfigure.md](https://github.com/WebexSamples/WebexStatusAPI/blob/main/docs/ImportAndConfigure.md) file with the required screenshots.

### Engage with Us

In case you have any further queries on this or if you are still facing some technical errors while trying to test the Status APIs, please reach out to our Developer Support team following the instructions provided on our [Webex Developer Support](https://developer.webex.com/support) page.

You can also join our [Webex Developer Community](https://community.cisco.com/t5/webex-for-developers/welcome-to-the-webex-for-developers-forum/m-p/4558386#M321) Forum, which has dedicated topics, discussion groups, and announcements. We encourage you to tell us about your experience using the Webex Status APIs in our community forum.
