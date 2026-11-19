---
type: Article
title: Introducing the Webex Web Calling SDK
canonical_url: https://developer.webex.com/blog/introducing-the-webex-web-calling-sdk
content_type: blog
date: '2024-01-25'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/introducing-the-webex-web-calling-sdk)

The Webex Developer Platform team is thrilled to unveil our Web Calling SDK, a new toolkit designed specifically for developers looking to integrate seamless calling features into their web applications using Webex. This SDK is a significant leap forward in our commitment to supplying robust, developer-friendly tools that enhance communication capabilities by now adding Calling workflows in addition to the existing Meetings and Messaging workflows. Whether you're building a sophisticated enterprise solution or a bespoke web application, our Web Calling SDK offers unparalleled flexibility, ease of use, and the high-quality performance that Webex is renowned for. This makes the Webex JS SDK repository a hub for major workflows available in the [Webex Collaboration Suite](https://www.webex.com/suite/collaboration-suite.html) (Calling, Meetings and Messaging).

In this post, we'll dive into the key features, benefits, and potential applications of this SDK, giving you all the information you need to start integrating state-of-the-art calling functionality into your web projects.

### Journey towards a Web Calling SDK

Over the last few years, the Webex application on desktop, mobile (Android & iOS) and Cisco devices supplied access to the calling capabilities of the Webex cloud. However, there were a few challenges here:

1. It required developers to cross-launch Webex to direct their users from their own applications when a user had to place or answer calls. Users needed to manually navigate back to the original applications during or when the call was completed. This led to a disconnected experience where a user’s attention moved away from their main application.
1. Users were tied to a particular platform. Developers had to add extra logic to support every platform such as Android, iOS, Windows, and Mac.
1. Linux and Chromebooks weren’t supported for the calling workflows.

Thus came the idea of supplying a toolkit for developers where they’d be able to integrate the world-class calling experience right into their applications. We chose the Web platform and WebRTC due to the ubiquitous availability of the underlying technologies.

### Building the SDK

This SDK is now publicly available as part of the [Webex JS SDK mono-repo](https://github.com/webex/webex-js-sdk) in GitHub. We added the [@webex/calling](https://github.com/webex/webex-js-sdk/tree/next/packages/calling) package to the mono-repo as it is familiar to existing developers. The calling package also depends on some of the plugins available in the Webex JS SDK. This made it a logical step to place it within the same repository.

### Key Features

The Web Calling SDK supplies a robust set of calling features to a developer and user. These features include:

- User and device registration with Webex Calling
- Making and receiving audio calls
- Hold, Resume and Transfer operations on established calls
- Switching background noise reduction on and off
- Mid-call device updates
- Retrieving call history for a user
- Retrieve voicemails and marking them read or unread
- Call quality metrics per call available on-demand (Chromium-based browsers)
- Managing user’s call preferences

A developer can build a full-fledged calling experience for their users within their existing applications by using the above features exposed in the Web Calling SDK.

### Real-World Applications

The Web Calling SDK can be used by developers across a multitude of verticals and use-cases. Some of the relevant deployment sweet spots we have seen during the extensive beta phase, include:

- **Telehealth** – Web applications that allow patients to login and place calls to their respective physician. Conversely, a portal for physicians where they can place to and receive calls from patients, consultants, and partners.
- **Finance** – The Calling SDK can be imported into applications and devices used for trades by stockbrokers to supply calling capabilities within the workspace's context.
- **CRM applications** – These applications can use calling capabilities for agents to place and receive calls within the application itself, allowing them to aid their customers quickly and efficiently. For instance, Webex for Salesforce is currently changing to consume this SDK.

<br/>

#### Productized Apps that use the Calling SDK

<br/>

- The [Webex Calling for Chrome](https://chromewebstore.google.com/detail/webex-calling-for-chrome/llllflgakifpdcmoanonghipldcpaggn?pli=1) extension leverages the Web Calling SDK to provide its capabilities. 
- Another consumer of the SDK is [Webex Calling for MS Teams](https://help.webex.com/en-us/article/ngmx08cb/Webex-Calling-for-Microsoft-Teams).

<br/>

### Integrating the Web Calling SDK into your projects

To get started, visit the [Webex Calling SDK](https://developer.webex.com/docs/sdks/webex-calling-sdk) page in the Webex Developer Portal. This will redirect you to the [QuickStart Guide](https://github.com/webex/webex-js-sdk/wiki/Quickstart-Guide-(Calling)) where you can find code snippets to begin importing and experimenting with the SDK.

You will need to have Webex Calling licenses to start integrating these flows into your application. Using a developer sandbox is a good way to start.

#### Best Practices

Some things to familiarize yourself with before using the SDK:

- OAuth flows used to [Authenticate with Webex](https://developer.webex.com/docs/integrations). This provides an access token with privileges to interact with the Webex cloud for services like calling, messaging, and meetings.
- [Kitchen sink page for Calling SDK](https://webex.github.io/webex-js-sdk/samples/calling/) – This sample application allows you to evaluate the various features exposed by the Web Calling SDK.
- [Sample applications](https://github.com/WebexSamples/web-calling-sdk-samples) that consume the Calling SDK

<br/>

### Looking Ahead

Exciting features are planned for future updates of the Web Calling SDK. Among these are

- Calling for guest users
- Video calls
- Calling widgets

<br/>

### Get Started Now

The Web Calling SDK, with its versatile and robust capabilities across various industries, from healthcare and education to finance and customer service is ready to take the industry to new heights. Its flexible integration and expansive feature set opens endless possibilities for developers to innovate and tailor solutions to the unique demands and workflows of different sectors.

### Need Some Help? We Got You Covered!

We are excited to provide you with support for these features. If you need help, the [Webex Developer Support Team](https://developer.webex.com/support) is standing by and happy to assist. You can also start or join a conversation on the [Webex for Developers Community Forum](https://cs.co/WebexDeveloperCommunity). Additionally, the [Issues](https://github.com/webex/webex-js-sdk/issues) page for our repository is the place to come to if you’re looking to give us some feedback.
