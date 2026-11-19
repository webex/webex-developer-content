---
type: Article
title: 'Webex Mobile SDK 3.10: Advanced Calling Capabilities'
canonical_url: https://developer.webex.com/blog/webex-mobile-sdk-3-10-advanced-calling-capabilities
content_type: blog
date: '2023-10-25'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/webex-mobile-sdk-3-10-advanced-calling-capabilities)

**What's happened:** With version 3.10.0, we’ve added advanced Webex Calling functionality to Mobile SDKs. At the SDK level, advanced features like background noise reduction and virtual backgrounds can be integrated into native apps for both iOS and Android.

### Support for 3 call legs

We have some exciting use cases to support assisted transfer when an agent already has 2 active calls. Consider a scenario where you work in a retail store for a technology company, and you receive a call from a customer named Alice who wants to enquire about certain products. After talking with Alice, you determine that her issue requires the expertise of another colleague, Peter. You inform Alice that you’re going to transfer her to Peter, who can help her with the issue. You call Peter to discuss the issue with him and provide some context. After discussing the issue with Peter, you return to the call with Alice. You let Alice know that Peter is ready and will assist her. You press the “transfer” button on your phone, and the call is connected to Peter for a smooth handoff.

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt3608dd03a8a6d6ef/Picture2.png)

### Support User Presence Status

Users can see the status of other participants Active, Inactive, DND, Call, Meeting, OOO in the call. It is essential in various collaboration platforms to help users understand when it’s appropriate to contact others and can help improve the efficiency of communication.

### Support Closed Captions

This feature will help the user understand the speaker and language being spoken during an instant (space) and scheduled meetings. For scenarios like Expert on Demand users conversing with subject matter experts from across the world seeking help and in cases where the user has trouble understanding the speaker and the language being spoken, closed captions provide real-time translation enabling conversations that were not possible before.

### Webex Calling

Using Webex Calling you can perform standard calling operations such as call hold, call transfer, call park, and accept incoming calls. When combined with other Webex services and devices, you’ve got the heart of a complete enterprise cloud calling and collaboration experience with minimal maintenance overhead and effective cost controls. 

Looking at an example scenario, let’s suppose a call is made to someone in a retail store, but an associate is not available at the front desk. Although no one is available at the desk, Webex Calling routes the call to the Webex-enabled app on the associate’s mobile phone. Upon call notification, the associate has the option to transfer a call to another associate. Some customers might need an expert to help them decide on product questions like purchasing furniture for their living room. 

It can also help communicate between different stores. For instance, if some items need to be urgently shipped but aren’t available at the originating store, the call can be transferred to another store’s shipping department to make sure the items are immediately available.

For more information on Webex Calling on mobile, check out our SDK documentation:

- [Developer Docs Android](https://developer.webex.com/docs/sdks/android)
- [Developer Docs iOS](https://developer.webex.com/docs/sdks/ios)

If you’ve got further questions related to the release, you can reach out to [Webex Developer Support](https://developer.webex.com/support).
