---
type: Article
title: Understanding Webex Meetings Application Platforms
canonical_url: https://developer.webex.com/blog/understanding-webex-meetings-application-platforms
content_type: blog
date: '2021-11-05'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/understanding-webex-meetings-application-platforms)

When exploring the Webex APIs and SDKs that are available here on the Webex for Developer portal, note there are two different Webex platforms documented for meetings applications, each representing a different Webex product.  One developer platform for the unified [Webex](https://www.webex.com/all-new-webex.html) client (formerly Webex Teams) and another platform for the [Webex Meetings](https://help.webex.com/ld-nyw95a4-CiscoWebexMeetings/Webex-Meetings) product. Webex is ultimately headed towards a singular platform as more functionality from Webex suite of products continues to be migrated to the unified Webex client. Until then, we give developers options for each platform. 

In general, we recommend you first consider building new meetings applications using the Webex SDKs and/or Widgets, as they leverage the latest unified API platform. Additionally, there are very limited licensing requirements for the unified platform, and most resources can be accessed even with a free Webex account. However, when it comes to apps that require automation of the *Webex Meetings* product, availability of certain features can be more dependent on the user's level of licensing. Let’s take a look at both for a better understanding on the differences of these two distinct Webex platforms.

### Webex Unified Client “Space Meeting” Apps

In the unified Webex client, meetings are associated with spaces. Developers can utilize the Webex APIs directly to create and manage spaces (aka "[rooms](https://developer.webex.com/docs/api/v1/rooms)") and manage meeting participants via [memberships](https://developer.webex.com/docs/api/v1/memberships). Alternatively, the [Webex Node.js SDK](https://developer.webex.com/docs/sdks/node) or [Java SDK](https://developer.webex.com/docs/sdks/java) can be used to streamline the API methods for managing meeting spaces and memberships. This "backend" functionality can be further extended, for example, by integrating with a calendaring solution, to facilitate a complete meeting scheduling system.

For the "frontside" of the meetings application, where video meetings are embedded and controlled, there are even more development options. This includes toolkits for all the popular browsers, as well as iOS and Android.

The quickest and easiest way to embed meetings into a web application is by leveraging [Webex Widgets](https://developer.webex.com/docs/widgets), which are built in *React*. Widgets allow developers to render space meeting functionality in a web application with just a few lines of code. Since Widgets keeps the same basic UI/UX design as the Webex client, there is not much tinkering required to embed a Webex meeting space.

For web applications that require a customized meeting interface, the [Webex Browser (JavaScript) SDK](https://developer.webex.com/docs/sdks/browser) allows embedding of video Meetings in a web app that is accessible from all the popular browsers - Chrome, Firefox, Edge or Safari, with no external plug-in required. The Browser SDK allows developers to tailor the UI/UX the way they want it, customizing the meeting experience for their particular app.

For the Webex [iOS](https://developer.webex.com/docs/sdks/ios) and [Android](https://developer.webex.com/docs/sdks/android) SDKs, developers can customize their Webex-enabled apps specifically for mobile devices. The key difference is the user experience on smaller screens, particularly using touch for input.

Again, the Webex Meetings REST APIs, as described in [this guide](https://developer.webex.com/docs/meetings), are specifically for the *Webex Meetings* platform; they do not interface with the unified client or Webex spaces as the SDKs and Widgets do. This is further explained in the next section.

### Webex Meetings Applications

The [Webex Meetings](https://developer.webex.com/docs/meetings) platform has separate developer interfaces. The Webex Meetings REST API allows developers to add basic meeting scheduling and management functions to their custom applications or websites. There are no SDKs for embedding Webex Meetings media into a 3rd party app; these APIs are essentially for automated scheduling and controls within the native Meetings client.

The Meetings APIs are accessible to all Webex accounts that are backed by [Cisco Webex Common Identity (CI)](https://help.webex.com/en-us/WBX000023841/How-Do-I-Know-if-a-Site-is-on-Common-Identity-CI). Keep in mind that certain API endpoints may only return a successful result if the the user as proper level of licensing. For example, if a Webex user license does not include the [meeting transcriptions](https://developer.webex.com/docs/api/v1/meeting-transcripts) feature, the API will return a failure stating that the user does not have access to that resource.

There are also some legacy applications that still leverage [Webex Meetings XML APIs](https://developer.cisco.com/docs/webex-xml-api-reference-guide/), which are now deprecated. Since the XML APIs where implemented in very different manner than the RESTful APIs supported on this site, the XML documentation is located on another developer portal, maintained by [Cisco DevNet](https://developer.cisco.com/). Mostly all of the the Webex XML endpoints have been migrated to the current RESTful APIs. While the Webex XML APIs will continue to be supported until further notice, the RESTful APIs found on this portal should now be considered the go-to for Webex developers moving forward. Any future Meetings API updates and new features will exclusively be for REST.

### Webex Developer Assistance is Easy to Find

We are really excited about all the cool new apps listed on the [Webex App Hub](https://apphub.webex.com/) from our partner and developer community. We want to see even more! Need help getting over any app dev hurdles? The amazing [Webex Developer Support Team](https://developer.webex.com/support) is standing by to assist. Remember, there is no need to be a paid Webex user to get fast dev support - our team is responsive to all and eager to help.
