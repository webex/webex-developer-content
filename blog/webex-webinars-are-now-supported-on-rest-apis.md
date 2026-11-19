---
type: Article
title: Webex Webinars are Now Supported on REST APIs
canonical_url: https://developer.webex.com/blog/webex-webinars-are-now-supported-on-rest-apis
content_type: blog
date: '2022-03-15'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/webex-webinars-are-now-supported-on-rest-apis)

The [Webex Webinars](https://www.webex.com/webinar.html) which replaces the Webex Classic Events Center, providing a plethora of features that were not available before. Webinars support a higher number of attendees who can leverage several new features such as real-time translation, closed captioning, reactions, simultaneous interpretation, breakout sessions, and the [Slido integration](https://apphub.webex.com/applications/slido-slido-55705) for polling, as well as Q&amp;A. Please visit [Webex Webinars](https://www.webex.com/webinar.html) for the full list of supported features.

To allow our customers to programmatically leverage and use Webinars, we are expanding the REST APIs to support Webinars-related functionality. The steps in a Webinar lifecycle are:

1. Creating a Webinar
1. Inviting participants to the Webinar
1. Managing registrations if registration is allowed
1. Retrieving assets and reports either during a running Webinar or after it ends

The following sections explain what you can do with the  Webinar REST APIs.

### Webinars Scheduling Management

Customers can schedule a Webinar via the API and can choose a regular Webinar or a Webinar with Webcast view. To understand the differences between a Webinar and Webcast, please check out this [article](https://help.webex.com/en-us/article/qbp6ek/Compare-experiences-in-Webex-Webinars). Customers can also handle scheduling management actions such as updating a Webinar’s settings, deleting a scheduled Webinar and retrieving a list of previously scheduled Webinars.

### Webinars Invitation Management

Using the APIs, customers can invite future attendees to the Webinar with the option to set them as panelists. Other invitation management functions are also provided such as updating, deleting or retrieving a list of people invited to a Webinar

### Webinars Registration Management

For a given Webinar, registration can be set as mandatory or optional with the option to auto-approve registrations. If registration is required, customers can choose which fields within the registration form are required and which should be optional. Customers can also approve, reject or even delete registrations. Finally, the API provides the ability to list registrants for a specific Webinar along with their detailed information so that customers can get updates on the registration progress.

### During and Post Webinars

While a Webinar is running, customers can retrieve a live list of the Webinar’s participants. That also applies once the Webinar ends to measure the Webinar’s adoption given the ratio of invited to registered users. The returned information about participants also includes the time they joined and left the Webinar to determine how long a participant has stayed in a Webinar, and thus measure engagement. Once a Webinar ends, customers can download the Webinar’s recordings and transcripts if they were enabled during the Webinar.

### Getting Started 

See the following articles for more information on using the Webex REST APIs in general and the Webinar APIs specifically:

- [How to start using REST APIs](https://developer.webex.com/docs/meetings)
- [Webex Webinars APIs Guide](https://developer.webex.com/docs/webinar-guide)
- [List of available REST APIs](https://developer.webex.com/docs/api/v1/meeting-invitees)

&nbsp;

### Your Feedback Matters

If you have feedback, suggestions, or you are encountering issues using the REST APIs, please reach out to our support team [https://developer.webex.com/support](https://developer.webex.com/support), and we will be very happy to help! In addition, feel free to post questions (and answers!) in our new [Webex Developer Community](https://community.cisco.com/t5/webex-for-developers/bd-p/disc-webex-developers).
