---
type: Article
title: Control Your Background in Webex Meetings Using Mobile SDKs
canonical_url: https://developer.webex.com/blog/control-your-background-using-mobile-sdks
content_type: blog
date: '2021-11-02'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/control-your-background-using-mobile-sdks)

Most of us are currently working remotely, and likely must attend several meetings per day. Examples include a student attending a virtual classroom meeting, or a patient who is attending a virtual visit with a care provider. In all cases, those users need a way to control their privacy and not worry about having an incorrect setup.

For that reason, we have extended the Webex iOS and Android Mobile SDKs to support the following features:

- Background blur
- Custom background images

The feature is available in release 3.2 for both SDKs and can be used when you join any Webex meeting using an application powered by our Webex Mobile SDKs.

![enter image description here][1]

&nbsp;

### More than Just a Feature

To ensure an excellent developer and end user experience, and knowing that developers don&#39;t have control over end user mobile devices, we have provided the following configuration options to support the custom/blur background feature:

- An API to check if the mobile device supports the feature. This allows developers to make sure that the hardware specifications of the mobile device support the minimum specifications for the feature to run smoothly.
- An alert for a high CPU utilization. This ensures that if the device where the feature is running has CPU utilization issues, there will be an alert so that developers can take suitable action to ensure a good user experience. In addition, to ensure that the CPU is not exhausted unnecessarily, the SDK is able to automatically customize the uploaded image size that to be used as a virtual background, so that the CPU is not overwhelmed by huge images sizes.
- Mobile Devices have limited storage, so we provide developers with the ability to set limits on the number of custom background images that their applications can support to avoid storage issues when they roll-out their applications in production.

&nbsp;

### Getting Started

First, test the feature using our Kitchen Sink application:

- [Kitchen Sink for iOS](https://github.com/webex/webex-ios-sdk-example) For iOS
- [Kitchen Sink for Android](https://github.com/webex/webex-android-sdk-example) For Android

To test the feature, follow the following steps:

1. Login to the Kitchen Sink app.
2. Click on **Extras** , then **Setup**.
3. Limit of the number of custom background images by setting **Virtual Background Limit** field.
4. Click the **brush** icon on the top right of the application to:
    1. Add a new image
    2. Delete an image
    3. Apply a particular image as a virtual background or blur the background
    
    ![enter image description here][2]

Then, explore our developers docs for both [iOS SDK](https://developer.webex.com/docs/sdks/ios) and [Android SDK](https://developer.webex.com/docs/sdks/android). You can find links to our GitHub repo as well as instructions on adding the SDKs to your mobile applications. We have also prepared a [Wiki](https://github.com/webex/webex-ios-sdk/wiki/Virtual-Background-Guide), as a quick guide on how to start using custom/virtual backgrounds **.**

&nbsp;

### Your Feedback Matters

If you have feedback, suggestions, or you are encountering issues using the SDKs or the background control features in particular, please reach out to our [support team](https://developer.webex.com/support), and we will be very happy to help!


  [1]: https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt6c5755542f906847/617c5db8e9faf1106303327b/blured-background.png
  [2]: https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltda006b3130c97edf/617c5db8b187491e7c56ef40/background-configuration.png
