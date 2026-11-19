---
type: Guide
title: iOS SDK | Overview
display_title: Overview
canonical_url: https://developer.webex.com/docs/sdks/ios-sdk-overview
content_type: documentation
product_group:
- webex-suite
categories:
- calling
- meeting
- messaging
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/ios-sdk-overview)

Build iOS apps with the **Webex iOS SDK**. Find supported features, requirements, samples, and API references.

## Webex iOS SDK Overview

[GitHub](<https://www.github.com/webex/webex-ios-sdk>)
[CocoaPods](<https://cocoapods.org/pods/WebexSDK>)

## Versions

* Current version: 3.17.0
* Previous major version: [2.8.0](https://developer.webex.com/docs/sdks/ios-v2)

## Features

* Audio and/or video 1:1 calling
* Group space calling
* Make and receive CUCM calls including hold/resume, transfer, merge
* Dial by email, Webex User ID, or SIP address
* Call and event controls, including DTMF
* Audio and video call control
* View content and video simultaneously
* Maximum bandwidth controls
* Receive and share content
* Message securely with threads
* Group call with three different views
* Multistream capability for controlling individual video layout
* Background Noise Reduction
* FedRAMP support
* Virtual Background
* Calendar Events
* Meeting Transcripts
* Network Quality Indicator
* Support for 1080p resolution in webex meetings, group space and 1:1 calling
* Multistream video pinning
* Unified Space Meetings
* Breakout session APIs and events for attendees
* "WebexSDK/Meeting" - A lightweight meeting-only SDK without calling features available 
* "WebexSDK/Wxc" - A lightweight SDK for WebexCalling
* PSTN noise removal for CUCM and Webex calling calls 
* Enhanced screen share API with ability to optimize for Video and Text  
* End to end encrypted meeting  
* Make and receive Webex Calling calls, including hold/resume, transfer, merge 
* Support for Webex calling new call payloads through webhook 
* Support for Closed Captions in a meeting 
* Support for Presence status
* Support for assisted transfer when the SDK client already has 2 active calls
* Support for calling events via mercury
* Support for moving a meeting from one client to another for the same user
* Support for USB Camera in iPADs for video calls
* "Webex-Message" - A lightweight SDK for message-only features
* Swift Package Manager distribution, in addition to CocoaPods New

## Resources

* [Github Repo](https://github.com/webex/webex-ios-sdk)
* [Change Log](https://github.com/webex/webex-ios-sdk/blob/master/CHANGELOG.md)
* [Guides to using SDK](https://github.com/webex/webex-ios-sdk/wiki)
* [Guide to migrating from v2.x to v3.x](https://github.com/webex/webex-ios-sdk/wiki/Migration-Guide-from-SDK-2.x-to-3.x)
* [Integrating the SDK using Swift Package Manager](https://github.com/webex/webex-ios-sdk/wiki/Integrating-SDK-with-App-using-Swift-Package-Manager)
* [Kitchen Sink Sample App](https://github.com/webex/webex-ios-sdk-example)
 
## Requirements



> **Warning**
>
> On December 2, 2026, CocoaPods trunk will stop accepting new pod versions. Existing CocoaPods integrations will keep working, but you must use Swift Package Manager to get later Webex iOS SDK releases. See the [CocoaPods trunk read-only plan](https://blog.cocoapods.org/CocoaPods-Specs-Repo/).



* Swift 5 or later
* Xcode 15 or later
* iOS 15 or later
* CocoaPods, or Swift Package Manager with WebexSDK 3.17.0 or later
* Webex Account

## Complete Demo App

A complete [demo application](https://github.com/webex/webex-ios-sdk-example) is available to see the complete functionality of the SDK.

## SDK API Reference

In-depth API reference information for the iOS SDK can be found [here](https://webex.github.io/webex-ios-sdk/)

## Troubleshooting the iOS SDK

If you're having trouble with the iOS SDK, here's some more information
to help troubleshoot the issue.

### Additional Logging

You can enable additional logging to your application to help narrow down any issues with the SDK.

#### Enabling console logging

```swift
webex.enableConsoleLogger = true
webex.logLevel = .verbose
```

### Upload Diagnostic Logs

The SDK supports uploading diagnostic logs directly to the Webex backend using `webex.uploadDiagnosticLogs()`, eliminating the need to manually extract and share log files. The uploaded bundle contains the same SDK diagnostic logs and media engine logs that are available through the existing `webex.getLogFileUrl()` API. For full details including response handling and error codes, see the [SDK Diagnostics Log Upload](https://github.com/webex/webex-ios-sdk/wiki/SDK-Diagnostics-Log-Upload) wiki guide.

### Firewall Ports

The iOS SDK makes use of the following network ports. If you're encountering connection issues, make sure there aren't any firewalls blocking or preventing communication over these ports:



| Service       | Protocol              | Port(s)                                       |
| ------------- | --------------------- | --------------------------------------------- |
| Messaging     | HTTPS                 | 443                                           |
| Notifications | WebSocket             | 443                                           |
| Calls         | HTTPS                 | 443                                           |
| Media         | RTP/SRTP over UDP/TCP | 33434-33598, 8000-8100 or 33434 (shared port) |

### App Crashes

If your app is crashing, crash reports may help you determine the root
cause. Please see Apple's [Understanding and Analyzing Application Crash
Reports](https://developer.apple.com/library/content/technotes/tn2151/_index.html)
for more information about diagnosing iOS app crashes.

The SDK also supports automatic crash reporting for SDK-related crashes. When enabled via `webex.isCrashReportingEnabled = true`, the SDK detects if a previous crash involved an SDK-owned library and automatically uploads the relevant diagnostics on the next app launch. For details on requirements, crash attribution, and limitations, see the [SDK Diagnostics Log Upload](https://github.com/webex/webex-ios-sdk/wiki/SDK-Diagnostics-Log-Upload) wiki guide.

## Support Policy

Please visit the [Webex API and SDK Support Policy](https://developer.webex.com/docs/webex-api-and-sdk-support-policy) page for details on our support and end of life policy for APIs and SDKs.

### Getting Support

If you're stumped, contact the [Webex Developer Support team](https://developer.webex.com/support) for more help with the SDK.
