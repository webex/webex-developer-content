---
type: Article
title: Webex Mobile SDKs – v3.5 Release
canonical_url: https://developer.webex.com/blog/webex-mobile-sdks-v3-5-release
content_type: blog
date: '2022-08-08'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/webex-mobile-sdks-v3-5-release)

The newest release of the Webex iOS and Android SDKs version 3.5 introduces features to continue bridging gaps between what’s possible with the Webex client Cisco builds and what’s possible with a Webex mobile integration that your team builds. With new additions including methods for capturing messaging events, categorizing media streams, and updated support for 1080p resolution, release v3.5 of the Webex Mobile SDKs gives developers more tools to create a rich user experience for any use case!

### TL;DR?

In this video, I discuss some of the new features included in version 3.5 and demonstrate their usage within our KitchenSink sample app:

<iframe src="https://app.vidcast.io/share/embed/ff454d52-5de9-4f52-9f70-720cb00fd973" width="100%" height="100%" title="Webex Mobile SDK v 3.5 Updates" frameborder="0" loading="lazy" allowfullscreen style="position:absolute; top:0; left: 0"></iframe>


&nbsp;

### Media Streams

Integrations which utilize Webex mobile SDKs to send real-time audio or video content now have an updated way to interface with streamed data. Version 3.5 introduces an object called `MediaStream`, which is bound to the user’s instantiated media stream. This simplifies the former approach of having separate objects for different media types. The `MediaStream`object has properties that can provide an application with relevant information about the type of media being streamed, the media’s quality, and events to capture any changes in quality. Paired with the Media Quality Indicator added in v3.4, these features allow applications to let users observe their own and others’ network status and subsequent media quality with a simple, familiar interface.

#### More with Media Streams

Aside from adding a new way to directly interact with a media stream, Webex iOS and Android SDKs v3.5 also add methods to read and update a media stream’s state from the top-level Call instance. Using the new `getMediaStreams()`method will return all open `MediaStream`instances within a call, something generally useful to even the most basic applications leveraging Webex’s audio and video capabilities.

These kinds of media streaming apps have also gained the ability to use the `setMediaStreamCategoryA`and `setMediaStreamCategoryB`methods to assign "Active" and secondary ("Category B") speaker types to media streams and update them whenever necessary. These additions are functional improvements to the way Webex integrations can implement smooth real-time communications experience for users. Both `setMediaStreamCatergory`methods, (A & B), have corresponding `removeMediaStreamCategory`methods to remove the "Active" and "Category-B" speaker streams.

Also in v3.5, the `MediaStreamAvailabilityEvent`event type on the `CallObserver`object can be triggered to report the availability of a particular media stream.

#### High-Definition 1080p Video

Release v3.5 adds updated support for the 1080p video resolution, giving developers the opportunity to "WOW!" their users with crisp video clarity via increased controls over the native iOS and Android camera interfaces. This opens the possibility for new, exciting use cases in the telehealth, education, fashion, and even photography.

#### Virtual Backgrounds

Integrations using Webex iOS or Android SDKs v3.5 can now implement virtual backgrounds in their app. Access to these virtual backgrounds gives developers building hybrid-work video applications an easy-to-use method of helping users invoke a level of privacy and professionalism in the modern workplace.

### Getting Started

There are plenty of resources available for developers who are ready to start using the Webex Mobile SDKs. Whether this is your first introduction to the Mobile SDKs, or whether you are just interested in implementing new features from v3.5 specifically, we’re excited to see what you build. For some examples, see:

- [Webex iOS SDK Example](https://github.com/webex/webex-ios-sdk-example)
- [Webex iOS SDK Documentation](https://developer.webex.com/docs/sdks/ios)
- [Webex Android SDK Example](https://github.com/webex/webex-android-sdk-example)
- [Webex Android SDK Documentation](https://developer.webex.com/docs/sdks/android)

&nbsp;

### Your Feedback Matters

If you have feedback, suggestions, or you are encountering issues using the REST APIs, please reach out to our support team [https://developer.webex.com/support](https://developer.webex.com/support) , and we will be happy to help! In addition, feel free to post questions (and answers) in our [Webex Developer Community](https://community.cisco.com/t5/webex-for-developers/bd-p/disc-webex-developers).
