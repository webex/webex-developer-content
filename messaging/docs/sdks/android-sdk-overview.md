---
type: Guide
title: Android SDK | Overview
display_title: Overview
canonical_url: https://developer.webex.com/docs/sdks/android-sdk-overview
content_type: documentation
product_group:
- webex-suite
categories:
- calling
- meeting
- messaging
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/android-sdk-overview)

Build Android apps with the **Webex Android SDK**. Find supported features, requirements, samples, and API references.

## Webex Android SDK Overview

[GitHub](<https://github.com/webex/webex-android-sdk>)

## Versions

* Current version: 3.17.0
* Previous major version: [2.8.0](https://developer.webex.com/docs/sdks/android-v2)

## What's new in Android SDK 3.17.0

Android SDK 3.17.0 includes the following updates and fixes:

* Updated the OpenSSL libraries used by the SDK.
* Improved hyperlink handling in message content.
* Improved SDK initialization when the SDK is used with dynamic feature modules.
* Fixed an issue that could cause a crash when adding a virtual background.
* Moved the Maven repository from `devhub.cisco.com` to `arti.anon.devhub-cloud.cisco.com`. Use the repository shown in the [calling integration guide](https://developer.webex.com/docs/sdks/android-calling-sdk-integrate-the-sdk), [meetings integration guide](https://developer.webex.com/docs/sdks/android-meetings-sdk-integrating-the-sdk), or [messaging integration guide](https://developer.webex.com/docs/sdks/android-messaging-sdk-integrate-the-sdk).

## Features

* Audio and/or video 1:1 calling
* Group space calling
* Dial by email, Webex User ID, or SIP address
* Call and event controls, including DTMF
* Audio and video call control
* View content and video simultaneously
* Maximum bandwidth controls
* Create Teams, Spaces, Memberships, and Messages
* Receive and share content
* Message securely with threads
* Group call with three different views
* Multistream capability for controlling individual video layout
* Background Noise Reduction
* Make and receive CUCM calls including hold/resume, transfer, merge
* FedRAMP support
* Virtual Background
* Calendar Events
* Meeting Transcripts
* Network Quality Indicator
* Support for 1080p resolution in webex meetings, group space and 1:1 calling
* Multistream video pinning
* Unified Space Meetings
* Breakout session APIs and events for attendees
* "WebexSDK-Meeting" - A lightweight meeting-only SDK without calling features available
* "Webex-Wxc" -  A lightweight SDK for WebexCalling 
* PSTN noise removal for CUCM and Webex calling calls
* Enhanced screen share API with ability to optimize for Video and Text
* End to end encrypted meeting
* Make and receive Webex Calling calls, including hold/resume, transfer, merge
* Support for Webex calling new call payloads through webhook 
* Support for Closed Captions in a meeting
* Support for Presence Status
* Support for assisted transfer when the SDK client already has 2 active calls
* Support for calling events via mercury 
* Support for rendering Live Annotations on shared screen in Meetings
* Support for moving a meeting from one client to another for the same user
* "Webex-Message" - A lightweight SDK for message-only features  New

## Resources

* [Github Repo](https://github.com/webex/webex-android-sdk)
* [Change Log](https://github.com/webex/webex-android-sdk/blob/master/CHANGELOG.md)
* [Guides to using SDK](https://github.com/webex/webex-android-sdk/wiki)
* [Guide to migrating from v2.x to v3.x](https://github.com/webex/webex-android-sdk/wiki/Migration-Guide-from-SDK-2.x-to-3.x)
* [Kitchen Sink Sample App](https://github.com/webex/webex-android-sdk-example)

## Requirements

* Android Studio 2025.2.1 or later
* Android SDK Tools 34 or later
* Android API Level 28 or later
* Java JDK 17
* Android NDK - 27.2.12479018+
* Kotlin - 2.1.+
* Gradle for dependency management
* Webex Account

## Complete Demo App

A complete [demo application](https://github.com/webex/webex-android-sdk-example) is available to see the complete functionality of the SDK.

## SDK API Reference

In-depth API reference information for the Android SDK can be found [here](https://webex.github.io/webex-android-sdk/)

## Troubleshooting the Android SDK

If you're having trouble with the Android SDK, here's some more information to help troubleshoot the issue.

### View the System Logs

The Webex Android SDK uses the Android system logger utility to collect log messages that will allow you to define problem areas when troubleshooting.

Use the `Logcat` command-line tool to collect, view, and filter all SDK logs. The Android SDK provides the option to display all messages or just the messages that indicate the most severe errors. Set the log level to `verbose` to display all errors. See [Write and View Logs with Logcat](https://developer.android.com/studio/debug/am-logcat.html) for more information.

```java
webex.setLogLevel(Webex.LogLevel.VERBOSE)
```
### Upload Diagnostic Logs

The SDK supports uploading diagnostic logs directly to the Webex backend using `webex.uploadDiagnosticLogs()`, eliminating the need to manually extract and share log files. The uploaded bundle contains the same SDK diagnostic logs, media engine logs, and any pending crash reports that are available through the existing `webex.getlogFileUri()` API. For full details including response handling and error codes, see the [SDK Diagnostics Log Upload](https://github.com/webex/webex-android-sdk/wiki/SDK-Diagnostics-Log-Upload) wiki guide.

### Firewall Ports

The Android SDK makes use of the following network ports. If you're encountering connection issues, make sure there aren't any firewalls blocking or preventing communication over these ports:



| Service | Protocol | Port(s) |
| ------- | -------- | ------- |
| Messaging | HTTPS | 443 |
| Notifications | WebSocket | 443 |
| Calls | HTTPS | 443 |
| Media | RTP/SRTP over UDP/TCP | 33434-33598, 8000-8100 or 33434 (shared port) |

### SDK Dependencies

For more information about dependencies of the Android SDK, please refer to their documentation:

* [Troubleshoot Android Studio](https://developer.android.com/studio/troubleshoot.html)
* [Android SDK Tools](https://developer.android.com/studio/command-line/index.html)
* [JDK Troubleshooting Guide](https://docs.oracle.com/javase/7/docs/webnotes/tsg/)
* [Gradle User Guide](https://docs.gradle.org/current/userguide/userguide.html)

### App Crashes

If your app is crashing, running a stack trace may help you determine the root cause. Please see Android’s [Diagnose the Crashes](https://developer.android.com/topic/performance/vitals/crash.html#diagnose_the_crashes) for more information about determining the cause of Android app crashes.

The SDK also supports automatic crash reporting for SDK-related native crashes. When enabled via `webex.enableCrashReporting(true)`, the SDK detects if a previous crash involved an SDK-owned library and automatically uploads the relevant diagnostics on the next app launch. This feature requires Android 12+ (API 31+) and is only available on release (non-debuggable) builds. For details on requirements, crash attribution, and limitations, see the [SDK Diagnostics Log Upload](https://github.com/webex/webex-android-sdk/wiki/SDK-Diagnostics-Log-Upload) wiki guide.

## Support Policy

Please visit the [Webex API and SDK Support Policy](https://developer.webex.com/docs/webex-api-and-sdk-support-policy) page for details on our support and end of life policy for APIs and SDKs.

### Getting Support

If you're stumped, contact the [Webex Developer Support team](https://developer.webex.com/support) for more help with the SDK.
