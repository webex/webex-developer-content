---
type: Article
title: Webex JavaScript SDK Now Has Real-Time Meeting Transcription
canonical_url: https://developer.webex.com/blog/webex-javascript-sdk-now-has-real-time-meeting-transcription
content_type: blog
date: '2022-01-11'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/webex-javascript-sdk-now-has-real-time-meeting-transcription)

There were many amazing new product features revealed at [WebexOne 2021](https://www.webex.com/webexone/index.html), including some fresh offerings for Webex developers. One of these new feature announcements that may have  slipped under the radar is for the [Webex Browser (JavaScript) SDK](https://developer.webex.com/docs/sdks/browser), which can now receive [real-time transcriptions for meetings](https://www.cisco.com/c/en/us/products/conferencing/webex-meetings/transcription.html). The transcriptions feature was previously only offered to Webex Meetings users and is now available to developers for meetings that take place in JavaScript authored apps! Besides providing live captions as participants talk, developers can also enable some other cool use cases such as:

- Automatic note taking
- Record action items
- Locate quotes and keywords
- Storing information for compliance

There are countless other game-changing ways that transcriptions can be leveraged in an application to get more out of meeting interactions.  What used to be difficult to implement in web applications can now be done quickly.

### Accurate &amp; Fast

Transcriptions in the Webex JavaScript SDK are powered by [Webex Assistant](https://help.webex.com/en-US/article/ygksov/Webex-Assistant-for-Webex-Meetings) to have exceptional precision, speed, and usability. They are generated through a speech-to-text engine that utilizes A.I. prediction models to vastly increase accuracy of the dialogue that is detected. As more words are spoken, the transcription is dynamically modified to structure sentences more precisely.  

Additionally, as part of the transcription output, Webex provides metadata that captures the identity of the speaker along with the exact timestamp, eliminating any guesswork. These transcriptions have practical uses right out of the gate. No need for time consuming post-processing – they are ready to go immediately.

Webex transcriptions are transmitted via a low latency WebSocket and received by the SDK as quickly as they are generated. This lightning-quick action allows developers to instantly expose the transcription data in their app for a variety of real-time uses. 

### Getting Started

Advanced transcriptions are available as part of [Webex Assistant](https://help.webex.com/en-US/article/ygksov/Webex-Assistant-for-Webex-Meetings) in the Webex Meetings product, for both scheduled and personal meeting room (PMR) meetings. Prior to receiving advanced transcriptions, the meeting host will first need to have [licensing provisioned for Webex Assistant](https://help.webex.com/en-US/article/6qoekm/Add-Licenses-for-Webex-Assistant-for-Webex-Meetings). Additionally, an administrator will need to enable the Webex Assistant feature on the user’s Webex site.

Once the feature is enabled on the site, Webex Assistant also needs to be turned-on in the meeting by the host. This now can be done programmatically through a new attribute of the [/meetingsPreferences API](https://developer.webex.com/docs/api/v1/meeting-preferences/update-scheduling-options): `enabledWebexAssistantByDefault`. Setting this parameter to true will turn-on Webex Assistant (by default) for all future meetings the user hosts.

From there, the SDK can receive Webex advanced transcriptions once the meeting starts by first initiating a [new transcription](https://webex.github.io/webex-js-sdk/api/#transcription) and then opening a low-latency [WebSocket connection](https://developer.webex.com/blog/using-websockets-with-the-webex-javascript-sdk) to listen for the proper transcription events. Each WebSocket event that is sent to the SDK will include a JSON payload containing the transcribed text, speaker names, and timestamp, which the developer can use accordingly in real-time or for historical purposes.

### Try it Out Now

Want to see it in action? We have a great way to check it out very quickly! When a meeting is initiated from the Webex JavaScript SDK [kitchen sink demo app](https://webexsamples.github.io/browser-sdk-samples/browser-plugin-meetings/) and Webex Assistant is enabled, real-time transcriptions can be generated inside a console on the demo configuration page.

When setting up the demo, before joining an active meeting, navigate to the ‘Meeting Controls’ section and click the button labeled ‘start receiving transcription’. When the users join the demo meeting, the real-time transcriptions will start to generate in the console underneath that button as speech is detected. Reference to other essential functions of the demo app can also be found on a [previous blog](https://developer.webex.com/blog/new-webex-sdk-updates-advanced-meeting-demo).

### Getting Help

As always, we have a lot of great developer resources to assist along the way, whether it is needing help leveraging transcriptions in the SDK, or questions about any of the other Webex APIs:

- The official GitHub repo for the Webex JavaScript SDK has documentation for enabling and handling transcriptions -  [https://webex.github.io/webex-js-sdk/api/#transcription](https://webex.github.io/webex-js-sdk/api/#transcription)
- More helpful information on the Webex Assistant feature: [https://help.webex.com/en-US/article/n5eooo0/Use-Webex-Assistant-in-Webex-Meetings-and-Events](https://help.webex.com/en-US/article/n5eooo0/Use-Webex-Assistant-in-Webex-Meetings-and-Events)
- Our amazing Webex Developer Support are available at all hours to help you with questions and for troubleshooting -  [https://developer.webex.com/support](https://developer.webex.com/support)
