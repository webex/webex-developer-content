---
type: Guide
title: iOS Messaging SDK | Integrate the SDK
display_title: Integrate the SDK
canonical_url: https://developer.webex.com/docs/sdks/ios-messaging-sdk-integrate-the-sdk
content_type: documentation
product_group:
- webex-suite
categories:
- messaging
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/ios-messaging-sdk-integrate-the-sdk)

You can integrate the Webex iOS SDK into your app using either [CocoaPods](http://cocoapods.org) or Swift Package Manager.

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

3. Create a new file, `Podfile`, with following content in your `MyWebexApp` project directory:

    ```bash
    source 'https://github.com/CocoaPods/Specs.git'
    ```

    - Full SDK : WebexSDK

    ```bash
    target 'WebexDemoApp' do
      platform :ios, '15.0'
      pod 'WebexSDK'
    end
    ```

4. Install the Webex iOS SDK from your `MyWebexApp` project directory:

    ```bash
    pod install
    ```

5. Add an entry, `GroupIdentifier`, to your app’s `Info.plist` with the value as your app's `GroupIdentifier` (required so we can retrieve a path to the local data warehouse).

6. Modify the `Signing & Capabilities` section in your Xcode project as follows:

   ![Signing and Capabilities](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt7596691b1414d4a7/signing_and_capabilities.png)

A sample app that implements this SDK with source code can be found at [https://github.com/webex/webex-ios-sdk-example](https://github.com/webex/webex-ios-sdk-example).



> **Info**
>
> The sample app is for illustration purposes only and it not meant for production environments.



## Using Swift Package Manager

From WebexSDK `3.17.0` onward, you can integrate the SDK with Swift Package Manager instead of CocoaPods. This requires Xcode 15 or later and an iOS 15 or later deployment target.

1. In Xcode, choose **File > Add Package Dependencies** and enter the package URL:

    ```text
    https://github.com/webex/webex-ios-sdk
    ```

2. Set the dependency rule to **Up to Next Major Version**, starting at `3.17.0`.

3. Add **one** WebexSDK product to your app target. For messaging-only use, add `WebexSDKMessage`, which is equivalent to `pod 'WebexSDK/Message'`. For the full SDK, add `WebexSDK`. Whichever product you choose, your code always uses `import WebexSDK`.

4. Complete the same app configuration as the CocoaPods flow: add the `GroupIdentifier` entry to your app's `Info.plist` and configure **Signing & Capabilities** with App Groups.
