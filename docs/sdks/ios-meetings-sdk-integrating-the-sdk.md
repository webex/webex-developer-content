---
type: Guide
title: iOS Meetings SDK | Integrating the SDK
display_title: Integrating the SDK
canonical_url: https://developer.webex.com/docs/sdks/ios-meetings-sdk-integrating-the-sdk
content_type: documentation
product_group:
- webex-suite
categories:
- meeting
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/ios-meetings-sdk-integrating-the-sdk)

You can integrate the Webex iOS SDK into your app using either CocoaPods or Swift Package Manager.

## Using CocoaPods



> **Warning**
>
> On December 2, 2026, CocoaPods trunk will stop accepting new pod versions. Existing CocoaPods integrations will keep working, but you must use Swift Package Manager to get later Webex iOS SDK releases. See the [CocoaPods trunk read-only plan](https://blog.cocoapods.org/CocoaPods-Specs-Repo/).





> **Info**
>
> Swift Package Manager is supported from WebexSDK 3.17.0 onward. Both channels deliver the same binaries. For Swift Package Manager, see [Using Swift Package Manager](#using-swift-package-manager).



Follow the steps in this article to create a new Xcode workspace that will use CocoaPods to install the SDK.

Assuming you already have an Xcode project, for example, `MyWebexApp`, here are the steps to integrate the Webex iOS SDK into your Xcode project using [CocoaPods](http://cocoapods.org):

1. Install CocoaPods:

    ```bash
    gem install cocoapods
    ```

2. Setup CocoaPods:

    ```bash
    pod setup
    ```

3. The Mobile iOS SDK comes in multiple flavors. If your use case requires only Webex meeting flows, consider using the size-optimized `WebexSDK/Meeting` SDK. If you need features beyond Meetings, consider using the full SDK, `WebexSDK`. Add the required library as a dependency for your app in the `Podfile`. Create a new file, `Podfile`, with the following content in your `MyWebexApp` project directory:

    ```ruby
    source 'https://github.com/CocoaPods/Specs.git'
    ```

    - Full SDK: `WebexSDK`

        ```text
        target 'WebexDemoApp' do
           platform :ios, '15.0'
           pod 'WebexSDK'
        end
        ```

    - Meetings SDK: `WebexSDK/Meeting`

        ```text
        target 'WebexDemoApp' do
           platform :ios, '15.0'
           pod 'WebexSDK/Meeting'
        end
        ```

    - Broadcast Extension: `WebexBroadcastExtensionKit`  (Required for screen sharing)

        ```text
        target 'MyWebexAppBroadcastExtension' do
           platform :ios, '15.0'
           pod 'WebexBroadcastExtensionKit'
        end
        ```

4. Install the Webex iOS SDK from your `MyWebexApp` project directory:

    ```bash
    pod install
    ```

5. Add an entry `GroupIdentifier` to your app’s `Info.plist` with the value set to your app's `GroupIdentifier`. This is required to obtain a path for storing the local data warehouse.

6. If you'll be using [WebexBroadcastExtensionKit](https://cocoapods.org/pods/WebexBroadcastExtensionKit), you also need to add an entry `GroupIdentifier` with the value as your app's `GroupIdentifier` to your **Broadcast Extension** target. This is required so that your app can communicate with the main app for screen sharing.

7. Modify the **Signing & Capabilities** section in your Xcode project as follows:

    ![Signing and capabilities dialog](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt2f5523da61dd19cb/signing_and_capabilities.png)

8. A sample app that implements this SDK, along with its source code, can be found at [https://github.com/webex/webex-ios-sdk-example](https://github.com/webex/webex-ios-sdk-example). This app is intended to showcase how to use the SDK methods and is not meant to be a production-grade application.

## Using Swift Package Manager

From WebexSDK `3.17.0` onward, you can integrate the SDK with Swift Package Manager instead of CocoaPods. This requires Xcode 15 or later and an iOS 15 or later deployment target.

1. In Xcode, choose **File > Add Package Dependencies** and enter the package URL:

    ```text
    https://github.com/webex/webex-ios-sdk
    ```

2. Set the dependency rule to **Up to Next Major Version**, starting at `3.17.0`.

3. Add **one** WebexSDK product to your app target. For meeting-only use, add `WebexSDKMeeting`, which is equivalent to `pod 'WebexSDK/Meeting'`. For the full SDK, add `WebexSDK`. Whichever product you choose, your code always uses `import WebexSDK`.

4. For screen sharing, add the `WebexBroadcastExtensionKit` product to your **Broadcast Upload Extension** target rather than the app target, and use `import WebexBroadcastExtensionKit` there.

5. Complete the same app configuration as the CocoaPods flow: add the `GroupIdentifier` entry to your app's `Info.plist`, add it to the Broadcast Extension target's `Info.plist` if you use screen sharing, and configure **Signing & Capabilities** with App Groups.
