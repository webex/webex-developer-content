---
type: Guide
title: Android Calling SDK | Webex Calling Introduction
display_title: Introduction
canonical_url: https://developer.webex.com/docs/sdks/android-calling-sdk-webex-calling-introduction
content_type: documentation
product_group:
- webex-suite
categories:
- calling
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/android-calling-sdk-webex-calling-introduction)

Webex Calling, a cloud-based phone system from Webex by Cisco, allows users to make and receive calls.

---

As of version 3.9.1, Android developers can now incorporate Webex calling capabilities into their own applications.

## License Requirements

A Webex Calling Professional license is required for using Webex calling features in the mobile SDK. Please contact [Sales](https://pricing.webex.com/in/en/) or [Support](https://developer.webex.com/support) for more information.

## Prerequisites

Make sure you meet the following prerequisites before using the SDK Webex calling features:

* Register an app in the Developer Portal as described in the following [link](https://developer.webex.com/docs/sdks/register-your-app).
* Follow the steps to integrate the SDK into your Android app as described in the following [link](https://developer.webex.com/docs/sdks/android-calling-sdk-integrate-the-sdk).
* For Webex Mobile SDK initialization and OAuth-based login configuration, refer to the first example in this [link](https://developer.webex.com/docs/sdks/android-calling-sdk-authorization).
* Incoming Webex Calling notifications are sent via webhooks to SDK-integrated mobile apps. The admin can set up a [firehose webhook](https://developer.webex.com/docs/webhooks#the-firehose-webhook) targeting `telephony_push` events. Upon receiving a webhook payload, it should be processed and forwarded from the backend server to the mobile app via APNS or FCM for handling.

## More Information

* [Basic Usage Guide](https://developer.webex.com/docs/sdks/android-calling-sdk-basic-webex-calling-usage)
* [Incoming Call Handling](https://developer.webex.com/android-calling-sdk-handle-incoming-webex-calling-calls)
* [Conference and Transfer](https://developer.webex.com/docs/sdks/android-calling-sdk-webex-calling-conferences-and-transfers)
* [PSTN Noise Removal](https://developer.webex.com/docs/sdks/android-calling-sdk-enable-incoming-pstn-call-noise-removal-for-webex-calling)
* [Additional Capabilities](https://developer.webex.com/docs/sdks/android-calling-sdk-additional-methods)
