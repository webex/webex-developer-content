---
type: Article
title: Supercharge Your App with Webex Mobile SDK 3.9.1
canonical_url: https://developer.webex.com/blog/supercharge-your-app-with-webex-mobile-sdk-3-9-1
content_type: blog
date: '2023-07-24'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/supercharge-your-app-with-webex-mobile-sdk-3-9-1)

> **Info**
>
> Kriti Jain, Engineering Product Manager, also contributed to this blog post.



In today's hyper-connected world, communication is the key to success. And to help you in this, Webex SDK 3.9.1 has just arrived, empowering your app with innovative calling features that will take your user experience to new heights! Let's delve into the exciting highlights of this release and discover how it can revolutionize your app's communication game.

### Webex Calling: Make Calls from Within Your App

Say hello to Webex Calling, the cloud-based phone system offered by Cisco as part of the Webex suite. Now, with the latest Webex Mobile SDK, you can seamlessly integrate calling capabilities into your own app and that too without incurring expenses and hassles of an on-prem solution. Imagine your users making and receiving crystal-clear calls without leaving your app's cozy environment. It's a communication revolution in the palm of their hands!

**NOTE**: Webex calling needs a professional license; for more information, please connect with the [Sales Team](https://pricing.webex.com/us/en/hybrid-work/calling).

But wait! Before you dive into the world of Webex Calling, there are a few prerequisites you need to check off:

1. Register your app in the [Developer Portal](https://github.com/webex/webex-android-sdk/wiki) (It's super easy, we promise!).
1. Integrate the SDK into your Android app by following the step-by-step guide provided [here](https://github.com/webex/webex-android-sdk/wiki).
1. To ensure a seamless experience, configure Webex Mobile SDK initialization and OAuth-based login with the help of the first example in this [link](https://github.com/webex/webex-android-sdk/wiki).

<br/>

#### Why should customers go for Webex Calling?

Using Webex Control Hub, customers can easily manage calling, meetings, and messaging from a single administrative console without the need to maintain a complicated and expensive back end to configure and administer. Control Hub also provides an interactive analytics dashboard with proactive insights into call quality and user experience. At the SDK level, advanced features like background noise reduction and virtual backgrounds can be integrated into native apps for both iOS and Android.

#### Webex Calling Use Cases

These are just a few example use cases for Webex Calling.

**Retail Customer Support**: A customer is calling a retail store, but an associate is not available at the front desk. Although no one is available at the desk, Webex Calling routes the call to the Webex-enabled app on the associate’s mobile phone. Upon call notification, the associate has the choice to transfer a call to another associate. Some customers might need an expert to help them decide on product questions like buying furniture for their living room.

Calling support can also be helpful in communicating between different stores. For instance, if some items need to be urgently shipped but aren’t available at the originating store, the call can be transferred to another store’s shipping department to make sure the items are immediately available.

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt9fa56e79fef646bd/64b82392bbc038f3ae776900/Picture2.png)

**Banking Customer Service**: Customers can reach out to the bank’s customer service team for help with accounts, transactions, or any other banking needs. Consider, however, that a customer needs to open a new bank account, and in the middle of the process the call gets disconnected. It can be cumbersome to reestablish the process if the same associate is not available on call back. However, with Webex Calling, since the calling functionality is present in the native mobile app of the associate, a customer can reconnect easily with the very same associate and resume the process without missing a beat.

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte59ea843f2e9a88b/64b823927b7f98494c9fdb27/Picture3.png)

### Webhook Mechanism: Never Miss a Call Notification Again

Introducing the webhook mechanism in Webex SDK 3.9.1—your secret weapon to streamline call notifications! Now, **developers can register their own REST endpoint**, which will be called whenever a call notification needs to be sent. Picture this: Cisco delivers the notification payload to your service, and it sends a notification to APNS or FCM. That means your app can retrieve incoming calls, even if it’s running in the foreground, background, or in the killed state. Talk about never missing a beat!

See the high-level architecture for **Android** in the image below:

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt088cee689c608cdc/64b82392d85ca61d3776e2f8/Picture4.png)

See the high-level architecture for **iOS** in the image below:

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltea04b013b6043fab/64b823920c8ace3c1e02e8c5/Picture5.png)

### Lightweight App Experience: Your App, Supercharged and Svelte

We understand the importance of keeping your app snappy and lightweight. That's why `WebexSDK` is now available as an `onDemand` Module on Android, using the Android Dynamic Feature Module. By embracing this technology, you can ensure that your app stays within the 150MB limit during installation. Modularize your app's features, let users download and install what they need on-demand, and watch your app soar!

For more details see:

- [Dynamic Feature Module Details](https://developer.android.com/guide/playcore/feature-delivery)
- [Use WebexSDK as onDemand Module](https://github.com/webex/webex-android-sdk/wiki/Use-WebexSDK-as-onDemand-Module-(using-Android-Dynamic-Feature-Module))

<br/>

### Dive deeper into the changes in SDK 3.9.1

For more detailed information on the features and changes in SDK 3.9.1 see:

- [iOS Change Log](https://github.com/webex/webex-ios-sdk/blob/3.9.1/CHANGELOG.md)
- [Android Change Log](https://github.com/webex/webex-android-sdk/blob/Release/3.9.1/CHANGELOG.md)
- New to Webex Mobile SDK? Check out the comprehensive setup and API documentation for [Android SDK](https://github.com/webex/webex-android-sdk/wiki) and [iOS SDK](https://github.com/webex/webex-ios-sdk/wiki) and visit our [SDK capabilities page for iOS](https://developer.webex.com/docs/sdks/ios) or [SDK capabilities page for Android](https://developer.webex.com/docs/sdks/android) to explore what all Webex Mobile SDK can do.
- How much does Webex Calling cost? Check out our [pricing](https://pricing.webex.com/us/en/hybrid-work/calling/) criteria.

<br/>

### Conclusion

The wait is over—Webex SDK 3.9.1 is here to transform your app into a communication powerhouse! With Webex Calling, your users can make and receive calls without ever leaving your app's ecosystem. The webhook mechanism ensures that call notifications reach your app flawlessly, and the lightweight app experience keeps your installation size in check.

### Need Some Help? We Got You Covered!

We are excited to provide you with support for these features. If you need help, the [Webex Developer Support Team](https://developer.webex.com/support) is standing by and happy to assist. You can also start or join a conversation on the [Webex for Developers Community Forum](https://cs.co/WebexDeveloperCommunity).
