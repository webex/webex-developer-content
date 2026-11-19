---
type: Article
title: Background Noise Reduction Added to Webex Browser SDK
canonical_url: https://developer.webex.com/blog/background-noise-reduction-added-to-webex-browser-sdk
content_type: blog
date: '2022-10-18'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/background-noise-reduction-added-to-webex-browser-sdk)

The Webex Browser SDK team has rolled out one of the major feature requests from our partners - the Background Noise Reduction (BNR) on Webex audio. Our advanced deep learning, speech science, and audio processing technology separates noise from human speech in any language. Your colleagues will hear you and not the noises in your workspace. This was made available to all the Browser SDK users at the end of August and is actively being integrated with a few partners on board. 

### The Feature

This feature rollout ensures the following:

- Enabling / Disabling BNR while the meeting is running
- Maintaining the state of BNR upon switching between audio input devices

BNR can be enabled / disabled only after joining the meeting. The SDK does not enable BNR by default. The BNR in the Browser SDK right now supports the following audio sample rates / number of samples:

- 16 kHz /  (128, 256)
- 32 kHz /  (128, 256, 512)
- 48 kHz / (128, 256, 512)

Any audio MediaStreamTrack that does not have one of the above sample rates are ignored with an error.
The SDK is supported in the following browsers:

- Desktop – Windows & Mac
  - Safari
  - Chrome
  - Firefox
  - Edge
- Mobile – Android & iOS
  - Chrome
  - Safari

Right now, the SDK does not support the following features:

- **Music mode**
  This is the scenario where one must play an instrument in a meeting while BNR is enabled. Right now, BNR assumes the music is a background noise and reduces it.

- **Optimize for my voice**
  This is the scenario where there is more than one member in the room and talking. In this scenario, BNR optimizes, voice of all members speaking rather than one.

These features are supported by the desktop and Webex devices right now and can be expected to be part of the Browser SDK at later point in time. 

### Release and Documentation

The BNR feature on the Browser SDK is available from version: `webex-js-sdk@2.19.1`

The documentation for this feature can be found at our [GitHub repository](https://github.com/webex/webex-js-sdk)'s wiki - [Background Noise Reduction | Webex Browser SDK](https://github.com/webex/webex-js-sdk/wiki/Background-Noise-Reduction). Furthermore, this feature can be tried using our public [Kitchen Sink Demo](https://webex.github.io/webex-js-sdk/samples/browser-plugin-meetings/) app.

If you are newly looking to integrate the Webex meetings SDK into your application, the [source code to our Kitchen Sink](https://github.com/webex/webex-js-sdk/tree/master/docs/samples/browser-plugin-meetings) is also available on our GitHub repository which can be used to quickly get started.

### Demo

https://app.vidcast.io/share/3f440def-3f7d-4eb1-83f2-7f3bd39208c3 


	<iframe src="https://app.vidcast.io/share/embed/3f440def-3f7d-4eb1-83f2-7f3bd39208c3" width="100%" height="100%" title="Webex Browser SDK - BNR Kitchen Sink Demo" frameborder="0" loading="lazy" allowfullscreen style="position:absolute; top:0; left: 0"></iframe>
