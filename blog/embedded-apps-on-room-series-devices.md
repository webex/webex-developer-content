---
type: Article
title: Embedded Apps on Room Series Devices
canonical_url: https://developer.webex.com/blog/embedded-apps-on-room-series-devices
content_type: blog
date: '2024-04-23'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/embedded-apps-on-room-series-devices)

Today if you are a Cisco device user, you can interact with [Embedded Apps](https://developer.webex.com/docs/embedded-apps) such as [Slido](https://www.slido.com/cisco-webex-polling), [Shared Timer](https://apphub.webex.com/applications/shared-timer-cisco-systems-22689), and [Miro](https://apphub.webex.com/applications/miro-miro-79512-22774) in meetings if you a join a meeting with touch-capable devices such as the Board and Desk Pro series.

Previously, users on [RoomOS](https://roomos.cisco.com/) devices were not able to view Embedded Apps once they were launched in a meeting. To enhance this experience, we are expanding the coverage of Embedded Apps on RoomOS devices as well. This will allow more users to be better involved in meetings, especially when Embedded Apps are initiated in those meetings.

### Feature details

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt6553652f2671a53d/ea-collab-and-preso-mode-blog-2.png)

#### RoomOS Devices

An Embedded app can have one of 2 orientations based on how they appear on the Webex desktop app once initiated. The first is the main view orientation. Main view orientation is for apps that appear in the stage of the Webex app. Example of main view apps are Miro and Mural. There is also the side panel orientation, where, once the app is initialized, it appears in the right-side panel of the Webex app.

Once a main view app is initialized from the Webex App desktop client (starting atbversion 44.12), users on Room OS device (starting at version 11.13.1.5) will be able to view a video stream of the initiator’s view (that is, what the initiator is seeing on their embedded app’s screen). Please note that this video stream has a lower priority than screen share, and therefore, if a user on the Webex app starts a screen share, that replaces the app’s video stream.

For side panel apps, in this first iteration we support the Slido and Shared Timer apps. Those apps are loaded on the Room OS devices on the right panel of the screen. Due to the nature of the Room OS device, users are not be able to participate in polls initiated by the Slido app. For that reason, the Slido app on the Room OS device will show a QR code, and users can scan it with mobile devices to participate in polls if desired.

#### DX, MX, and SX Series Devices

The same criteria apply to DX, MX, and SX devices, the only difference being that the Slido and Shared timer apps are not supported in this first iteration while apps rendered in the Webex main view are.

&#xa0;

### Need Some Help? We Got You Covered!

We are excited to provide you with support for these features. If you need help, the [Webex Developer Support Team](https://developer.webex.com/support) is standing by and happy to assist. You can also start or join a conversation on the [Webex for Developers Community Forum](https://cs.co/WebexDeveloperCommunity).
