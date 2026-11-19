---
type: Article
title: Announcing the Multistream Feature in Webex Web Meetings SDK
canonical_url: https://developer.webex.com/blog/announcing-the-multistream-feature-in-webex-web-meetings-sdk
content_type: blog
date: '2024-09-24'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/announcing-the-multistream-feature-in-webex-web-meetings-sdk)

The [Webex Web Meetings SDK](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-introduction) is a powerful tool designed to enable developers to seamlessly integrate Webex meeting capabilities into their web applications. With this SDK, developers can create, join, and manage Webex meetings directly from their web-based platforms, delivering a rich and interactive video conferencing experience. The SDK provides a comprehensive set of APIs and functionalities, including high-quality video and audio, screen sharing, meeting controls, and participant management.

### What is Multistream?

In a traditional transcoded meeting, all video streams from participants are processed and combined into a single composite video stream before being sent to each participant. This approach simplifies video processing but has limitations in flexibility and quality.

The Multistream feature allows developers to receive multiple individual video streams directly from a Webex meeting. This capability enables more advanced video layouts and customized views, making it easier to create dynamic and engaging video conferencing experiences.

### Key Benefits of Multistream

These are the key benefits of the Webex Multistream technology:

- **Enhanced Video Layouts:** With the ability to handle multiple streams, you can now create sophisticated video layouts, such as grids, active speaker views, and custom views tailored to specific use cases like in education, where teachers can create layouts that show the main lecture feed along with student video feeds, enabling more interactive and engaging lessons.
- **Optimized Bandwidth Usage**: Control over individual streams helps in optimizing bandwidth usage by only subscribing to the streams you need. This is particularly useful in corporate settings, where large meetings and webinars often involve many participants, allowing you to focus bandwidth on key speakers and relevant departments, ensuring smooth video quality and effective communication.
- **Improved User Experience**: Provide a more interactive and immersive meeting experience by using dynamic layouts as each participant's video feed is received as a separate stream. For example, in Media and Entertainment, you can offer viewers a richer experience with multiple perspectives during live event broadcasts, making the experience more engaging and dynamic.

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltafb3245399f04b5b/multi-stream-blog-2.png)
**Figure 1:** Multistream in our Kitchen Sink app demonstrating Stage with thumbnails

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt0b120b97bfac8cab/multi-stream-blog-3.png)
**Figure 2:** Multistream in our Kitchen Sink app demonstrating all equal panes (max 9).

### Documentation

This Multistream feature in the Browser SDK is available from version: `webex-js-sdk@3.3.1`. For detailed information, see:

- [Quick Start Guide:](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-multistream-quick-start) Provides a step-by-step process to integrate Multistream capabilities into your Webex application.
- [Comprehensive Guide:](https://developer.webex.com/docs/multistream-comprehensive-guide) Dives deeper into the Multistream functionality, offering advanced insights and best practices.



> **Info**
>
> To try out the Multistream feature, check out our [Kitchen Sink](https://webex.github.io/webex-js-sdk/samples/browser-plugin-meetings/) app!



### Other Helpful Links

For additional information see:

- [Migrating from SDK V1/V2 to V3](https://github.com/webex/webex-js-sdk/wiki/Migrating-SDK-Version-1-or-Version-2-to-Version-3)
- [Source code of Kitchen Sink app](https://github.com/webex/webex-js-sdk/tree/next/docs/samples)

<br/>

### Vidcast Demo

Check out our demo Vidcast:


  <iframe src="https://app.vidcast.io/share/embed/c0ea5361-6bae-46ef-835f-0694a3046853" width="100%" height="100%" title="Multistream Using the Webex SDKs" frameborder="0" loading="lazy" allowfullscreen style="position:absolute; top:0; left: 0;border: solid; border-radius:12px">
  </iframe>


<br/>

### Customer Testimonial

Here, Jason Ruane from Cives shares his experience with the Multistream technology and how Cives leverages it in their solutions:

"At [Cives](https://cives.ai/), integrating the Multistream feature into our flagship solution, Courts for Webex, has been a transformative step forward. This technology empowered us to develop a highly customized courtroom synoptic view, elevating the virtual courtroom experience.

"By utilizing multiple individual video streams, we crafted dynamic, real-time layouts tailored to the specific needs of judges, attorneys, and witnesses. This approach not only optimized bandwidth but also ensured that essential video feeds remained in focus, creating an immersive environment that meets the stringent requirements of modern judicial proceedings.

"Furthermore, [Cives](https://x.com/civesofficial) leveraged Multistream audio to route individual audio streams directly to court recording solutions, guaranteeing precise and dependable documentation for every session."

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt95765319b3a653b7/multi-stream-blog-4.png)
**Figure 3:** Courts for Webex.

### Conclusion

The new Multistream feature in the Webex Web Meetings SDK opens up a world of possibilities for developers looking to enhance their video conferencing applications. We encourage you to explore the documentation, try out the examples, and start integrating Multistream into your Webex projects today.

### Need Some Help? We Got You Covered!

We are excited to provide you with support for these features. If you need help, the [Webex Developer Support Team](https://developer.webex.com/support) is standing by and happy to assist. You can also start or join a conversation on the [Webex for Developers Community Forum](https://cs.co/WebexDeveloperCommunity).
