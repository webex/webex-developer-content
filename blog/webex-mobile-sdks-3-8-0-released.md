---
type: Article
title: Webex Mobile SDKs 3.8.0 Released
canonical_url: https://developer.webex.com/blog/webex-mobile-sdks-3-8-0-released
content_type: blog
date: '2023-02-23'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/webex-mobile-sdks-3-8-0-released)

The Webex Mobile SDKs for iOS and Android have released a new version, version 3.8.0, which has some important features for developers. The two major features that we are excited about are the meeting only SDK and the new beta for the Webex Calling support!

### Meetings-only SDK

If your application is only utilizing Webex Meetings in the mobile SDKs, you now can cherry-pick just that functionality to reduce the file size of the SDK.

The Meetings-only SDK reduces file sizes by:

- AAR size (Universal, as user will download this only) reduced by 214 - 186 = 28 MB
- APK size (arm 64) reduced by 57 - 46 = 11 MB
- Installation size (arm 64) reduced by 218 - 160 = 58MB.

An iOS and Android SDK (Software Development Kit) that is optimized to have a smaller file size can have several benefits for developers who use it in their apps. These benefits include:

- Faster download and installation times: smaller file sizes mean that the SDK can be downloaded and installed more quickly, which can save time for developers and reduce the chance of installation errors.
- Reduced storage space requirements: smaller file sizes also mean that the SDK takes up less storage space on the device, which can be especially important for apps that are designed for devices with limited storage capacity.
- Lower app sizes: When developers include the SDK in their apps, the app size will be smaller, which can be beneficial for app store ranking, and also for users with limited storage.
- Lower network usage: When developers update the app, the smaller size of the SDK can help reduce network usage and data consumption, which can be especially important for apps that are used in areas with limited or expensive network coverage.
- Better user experience: smaller file sizes can help improve the user experience by reducing the time it takes to download and install the app, and by reducing the amount of storage space the app requires.

Overall, reducing the file size of an SDK can have a positive impact on the performance, usability and user experience of apps that use it. Learn how to use this Meetings-only SDK here:

- Android: <https://github.com/webex/webex-android-sdk/wiki/Integrating-SDK-with-App>
- iOS: <https://github.com/webex/webex-ios-sdk/wiki/Integrating-SDK-with-App>

&nbsp;

### Calling SDK

A much asked for feature from Webex Calling customers was the support for Webex Calling in our mobile SDKs. We’re happy to announce that the early limited trials are now available for our Webex Calling Mobile SDK! If you’re interested in trialing this feature, please reach out to product manager Kriti Jain on [this thread](https://community.cisco.com/t5/webex-for-developers/mobile-sdk-webex-calling-basic-features/td-p/4753424) in our Developers Community Forum.

The usage guides for the Calling Mobile SDKs can be found here:

- [https://github.com/webex/webex-android-sdk/wiki/Webex-Calling-Usage-Guide](https://github.com/webex/webex-android-sdk/wiki/Webex-Calling-Usage-Guide)
- [https://github.com/webex/webex-ios-sdk/wiki/Webex-Calling-using-Mobile-SDKs](https://github.com/webex/webex-ios-sdk/wiki/Webex-Calling-using-Mobile-SDKs)

&nbsp;

### Need Some Help? We Got You Covered!

We are excited to provide you with support for these features. If you need help, the [Webex Developer Support Team](https://developer.webex.com/support) is standing by and happy to assist. You can also start or join a conversation on the [Webex for Developers Community Forum](https://cs.co/WebexDeveloperCommunity)!
