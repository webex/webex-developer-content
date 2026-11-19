---
type: Article
title: Webex for Developer Newsletter Feb 2022
canonical_url: https://developer.webex.com/blog/webex-for-developer-newsletter-feb-2022
content_type: blog
date: '2022-02-01'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/webex-for-developer-newsletter-feb-2022)

### Revisiting the End of 2021 and Jumping into a Busy 2022

The *Webex for Developers* platform has generated a lot of news and activity through the end of 2021 and into the new year 2022. From new product launches to important platform updates, there is certainly a lot going on. To get a glimpse of how enormously important application developers are to Webex, let’s look back at some of the recent headlines and highlights that are focused on them.

But before we do that, it’s always great to see the cool innovations that our partners are bringing to market. In our **Webex Partner Spotlight** this month is Poll Everywhere. [Poll Everywhere](https://apphub.webex.com/applications/poll-everywhere-poll-everywhere-53597) built and deployed a Webex Embedded App to enhance the hybrid work experience, by turning presentations into inclusive conversations. Read the [blog](https://developer.webex.com/blog/building-the-poll-everywhere-webex-embedded-app) for a walkthrough of the code and see how they created their app. Well done and congrats to the Poll Everywhere team - very cool stuff!

### Webex One – Developer Track Highlights

At the end of October 2021, Cisco held the second annual [Webex One](https://www.webex.com/webexone/index.html) virtual event. The Webex for Developers team had a lot of great announcements as part of a new track that showcased Webex applications and extensibility. You can learn more about this in the [Webex One developer track wrap-up blog](https://developer.webex.com/blog/webex-one-developer-track-wrap-up). Here are some of the main takeaways:

#### New Product Announcement: Webex Connect CPaaS (Communications Platform as a Service)

A new CPaaS offering was unveiled in one of the first developer-track sessions, called **Webex Connect**. This new product announcement should truly excite developers. Webex Connect CPaaS offers powerful, easy to use APIs and dev tools, to build smarter interactions across multiple channels, such as video, voice, and messaging.

Webex Connect is primarily built on the former [imiconnect platform](https://imimobile.com/products/imiconnect), as part of Cisco’s **imi**mobile acquisition. One of the best parts of CPaaS is there’s no licensing or similar barriers to entry for developers to build applications. Just sign up for the service and hit the ground running! You can discover more about Webex Connect CPaaS [here](https://www.webex.com/products/cpaas.html).

#### New: Webex Assistant for Developers

We know many developers have been clamoring to build apps that can leverage Webex Assistant features and skills. In another Webex One developer-track session, there were a couple more exciting updates announced for developers, pertaining to Webex Assistant AI.

First, real-time transcriptions powered by Webex Assistant, is now available in the Webex JavaScript SDK. Real-time transcriptions were previously only offered to users of Webex Meetings app and are now available to developers to add to their own JavaScript authored app. Webex transcriptions can empower app use cases that require real-time functionality for speaker captions or automated note taking, for example.

Also announced was the [Webex Assistant Skills Platform](https://skills-developer.intelligence.webex.com/). Webex Assistant skills are voice-driven applications that relay audio and web content back to Cisco Webex Room Kit, Cisco Webex Board, and Cisco Webex Desk Pro devices. With the announcement of this developer platform for Webex Assistant, skills can also be built and deployed to give voice functionality to new or existing applications and integrations. For example, the [Jarvis Room Control Skill](https://skills-developer.intelligence.webex.com/content/Jarvis-Skill.mp4), which is a home/office automation skill that controls various, real-life IoT connected devices.

You can learn more about [Webex Assistant Skills programmability](https://developer.webex.com/docs/webex-assistant-skills-overview) on the Webex Developer portal.

#### New Product Announcement: Webex Embedded Apps

Another huge product announcement that came out in a later Webex One developer session is the[Webex Embedded Apps Framework](https://developer.webex.com/docs/embedded-apps). This framework lets developers easily integrate web applications into Webex meetings and spaces, enabling a higher level of collaboration for users.

In many instances, information that users need to reference resides outside of Webex in other web-based applications, requiring them to switch contexts and focus between Webex and the external application. Webex Embedded Apps surfaces those web applications directly within a Webex meeting or messaging space, enabling other participants to access and interact with it directly.

You can learn more about the Webex Embedded Apps announcement in this [blog post](https://blog.webex.com/messaging-chat/unlock-frictionless-collaboration-with-apps-right-inside-webex/).

### More Webex API and SDK Updates

Riding the momentum of Webex One, updates to the developer platform continued at a strong pace. Let’s look at the most notable ones that were recently released: 

#### New: Webex Meetings Widget

The Webex Meetings Widget provides functionality of the native client that can be embedded into any web-based application with just a few lines of code. With this Meetings Widget, developers can quickly add features to join any Webex meeting type, share a screen, manage media devices and more.

To see how it easy it is, head over to our developer portal again for [Webex Widgets overview](https://developer.webex.com/docs/widgets#meetings-widget-).

#### New: Messaging Announcement Mode API

Webex bots and integrations can now create moderated messaging spaces in announcement-mode. This allows apps to share important information or broadcast notifications without any distraction from other conversations.

To learn more about this new capability, check out the [announcement blog](https://developer.webex.com/blog/introducing-the-webex-messaging-announcement-mode-api).

#### New: Custom backgrounds in Webex Mobile SDKs

Since remote working and video meetings have become the norm, it’s more crucial than ever for users to keep control of their privacy. This can be even more important for users joining meetings on a mobile device, perhaps from a sensitive location. While custom backgrounds and blur have already been available in the Webex mobile app, they are now available to developers in the Webex [Android](https://developer.webex.com/docs/sdks/android) and [iOS](https://developer.webex.com/docs/sdks/ios) SDKs. Now those users can keep their video turned on in just about any environment.

For more information on how this works, see this [blog post](https://developer.webex.com/blog/control-your-background-using-mobile-sdks) for a full rundown.

#### More Webex for Developer Enhancements

There are a couple other noteworthy updates to the API and developer portal released recently. First, coming off the WebexOne announcement on the availability of advanced transcriptions in the Webex JavaScript SDK, a new attribute has been added to the [/meetingsPreferences API](https://developer.webex.com/docs/api/v1/meeting-preferences/update-scheduling-options) to help developers better leverage this feature. This essentially allows developers to programmatically enable Webex Assistant and closed captions for the meeting host, instead of the host having to turn it on manually in the client. You can read more about receiving transcriptions in the Webex JavaScript SDK **here**.

Speaking of transcriptions, [/webhooks](https://developer.webex.com/docs/api/v1/webhooks) now supports a new resource called `meetingTranscripts` for the **transcripts: created** event. Now apps can be notified as soon as the transcription is ready to quickly take quick action.

As an additional reminder, [the Webex for Developer changelog](https://developer.webex.com/docs/api/changelog) is available for a complete listing of the latest the Webex API updates and feature releases.

### Webex Developer Portal Updates 

You may have noticed that the user interface on the Webex for Developers site has gone through a bit refresh recently, to reflect the look and feel of the new Webex app. Besides the overall improvements to the interface, there has also been some great additions to our documentations, such as:

- [New Webex for Developer FAQ](https://developer.webex.com/docs/frequently-asked-questions)
- [Webex Connect API overview](https://developer.webex.com/docs/webex-connect-api-overview)
- [Webex Embedded Apps Developer Guide](https://developer.webex.com/docs/embedded-apps)
- [Webex Meetings Widget Developer Guide](https://developer.webex.com/docs/widgets#meetings-widget-)
- [Webex Assistant Skills Developer Guide](https://developer.webex.com/docs/webex-assistant-skills-guide)

&nbsp;

### Webex Developer Blog Updates 

Along with the new documentation, we have also published a slew of new blog posts on a variety of Webex developer topics:

- [Give Your Webex Bot some $uperpowers](https://developer.webex.com/blog/give-your-webex-bot-some-superpowers)
- [Using OAuth with Webex in Your React Application](https://developer.webex.com/blog/using-oauth-with-webex-in-your-react-application)
- [Face &amp; Hand Tracking in Webex](https://developer.webex.com/blog/face-hand-tracking-in-webex)
- [Convenient Webex OAuth for Laravel Projects with Socialite](https://developer.webex.com/blog/convenient-webex-oauth-for-laravel-projects-with-socialite)
- [Understanding Webex Meetings Application Platforms](https://developer.webex.com/blog/understanding-webex-meetings-application-platforms)

&nbsp;

### New Product Announcement: Programmatic Contact Center

Every business and every customer journey is unique. The [Webex Customer Experience platform](https://www.webex.com/contact-center.html) provides an optimal balance of enterprise-grade, out-of-box customer experience solutions that are now fully programmable. This makes it easy to deliver precise and personalized customer experiences, for your customers.

The launch of the new APIs and developer portal announced at WebexOne, makes this vision a reality. Developers now have access to:

- Webex Contact Center APIs
- AI APIs
- Customer Journey APIs
- Desktop SDKs
- How-to Guides

…and we are just getting started!

Partners and Customers can register their apps with a single click, and use these APIs to provide a personalized service, tie together siloed business systems, build complimenting services, and access rich customer experience data.

Check out the all-new [Webex CX developer portal](https://developer.webex.com/webex-contact-center/docs) to learn more and help build an ecosystem that adds value to our core offering.

### New - Webex Evangelism Team Webinar Series

Webex Developer Evangelist Team will be hosting a series of public webinars starting in February, with topics geared towards developers and Webex extensibility. 

The first webinar in the series is an introductory walkthrough of Webex apps, integrations, and developer platform. In this webinar, you will get to know the Webex developer product portfolio, tools, and resources, for building seamless integrations. We’ll explore different application types and popular use cases that highlight how developers can leverage the Webex platform to enhance the user experience.

[Click here to register](https://cisco.webex.com/cisco/j.php?RGID=r127bacab5305d851334a8f3549631a82) for the February webinar **Webex for Developers: Intro to Webex Apps and Integrations**.

### Follow us on Twitter!

Lastly, don’t forget to follow [@WebexDevs](https://twitter.com/WebexDevs) on Twitter to up to date on the latest news and announcements. We look forward to connecting with you there!
