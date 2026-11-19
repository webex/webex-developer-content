---
type: Guide
title: Web Calling SDK | Core Concepts
display_title: Core Concepts
canonical_url: https://developer.webex.com/docs/sdks/webex-calling-sdk-web-core-concepts
content_type: documentation
product_group:
- webex-suite
categories:
- calling
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/webex-calling-sdk-web-core-concepts)

Prior to diving into the calling features of the Webex JS SDK, it's essential for developers to grasp a few fundamental concepts.

## Access Token

The access token serves as a secure digital key that grants authorized access to various Webex services and resources. This token is a vital component of authentication and authorization mechanisms, ensuring that only trusted entities can interact with Webex on behalf of a user or application. Developers can obtain and utilize access tokens to initialize and consume the calling features available on the Webex JS SDK.

## Calling

The `Calling` object serves as the developer's primary gateway, offering access to a range of essential features, including Calls, Voicemail, Contacts, Call History, and Call Settings. Developers initiate the `Calling` instance by configuring the SDK, and it additionally provides developers with the capability to create audio streams.

## Calling Client

The `CallingClient` module, housed within the `Calling` object, plays a pivotal role in developer authorization for establishing a Webex Calling endpoint. This endpoint facilitates the seamless exchange of calls with the Webex cloud, both outgoing and incoming. After an administrator successfully provisions a user within a Webex Calling licensed organization, the `CallingClient` module can be leveraged to generate the requisite endpoint associated with that user.

## Line

The `Line` feature in the `CallingClient` module acts as a virtual phone line, enabling the handling of both incoming and outgoing calls. This feature offers configurable settings and controls, empowering developers to manage multiple calls on different lines for an individual user.



> **Info**
>
> As of October 1, 2023, the SDK currently supports only a single `Line` within the `CallingClient`. The capability to support multiple lines is planned for a future release.



## Call

Within the `CallingClient` module, the `Call` object serves as the operational unit for a specific call, offering a variety of methods to manage call characteristics such as direction, status, and participant details. In addition to basic actions like initiating, answering, and terminating calls, the `Call` object also supports supplementary services like placing calls on hold, resuming them, and facilitating different types of call transfers, enhancing the feature set for real-time voice and video communications in your applications.
