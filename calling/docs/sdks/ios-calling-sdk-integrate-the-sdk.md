---
type: Guide
title: iOS Calling SDK | Integrate the SDK
display_title: Integrate the SDK
canonical_url: https://developer.webex.com/docs/sdks/ios-calling-sdk-integrate-the-sdk
content_type: documentation
product_group:
- webex-suite
categories:
- calling
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/ios-calling-sdk-integrate-the-sdk)

You can integrate the Webex iOS SDK into your app using either [CocoaPods](https://guides.cocoapods.org/using/getting-started.html) or Swift Package Manager.

## Using CocoaPods



> **Warning**
>
> On December 2, 2026, CocoaPods trunk will stop accepting new pod versions. Existing CocoaPods integrations will keep working, but you must use Swift Package Manager to get later Webex iOS SDK releases. See the [CocoaPods trunk read-only plan](https://blog.cocoapods.org/CocoaPods-Specs-Repo/).





> **Info**
>
> Swift Package Manager is supported from WebexSDK 3.17.0 onward. Both channels deliver the same binaries. For Swift Package Manager, see [Using Swift Package Manager](#using-swift-package-manager).



Assuming you already have an Xcode project, for example, *MyWebexApp*, for your iOS app, here are the steps to integrate the Webex iOS SDK into your Xcode project using [CocoaPods](http://cocoapods.org):

1. Install CocoaPods:

    ```bash
    gem install cocoapods
    ```

2. Setup CocoaPods:

    ```bash
    pod setup
    ```

3. The Mobile iOS SDK is available in multiple flavors. If your use case involves only Webex Calling flows, consider using the size-optimized `WebexSDK/Wxc` SDK. For features beyond Webex Calling and for UCM calling, use the full SDK `WebexSDK`. Add the required library as a dependency in your app's `Podfile`. Create a new file named `Podfile` with the following content in your *MyWebexApp* project directory:

    ```bash
    source 'https://github.com/CocoaPods/Specs.git'
    ```

    - **Full SDK : WebexSDK**

    ```bash
   target 'WebexDemoApp' do
      platform :ios, '15.0'
      pod 'WebexSDK'
   end
    ```

    - **Meeting SDK : WebexSDK**

    ```bash
   target 'WebexDemoApp' do
      platform :ios, '15.0'
      pod 'WebexSDK/Meeting'
   end
    ```

   - **WebexCalling SDK :WebexSDK/Wxc**

    ```bash
   target 'WebexDemoApp' do
      platform :ios, '15.0'
      pod 'WebexSDK/Wxc'
   end
    ```

4. Install the Webex iOS SDK from your *MyWebexApp* project directory:

    ```bash
    pod install
    ```

5. In your app's `Info.plist`, add an entry named `GroupIdentifier` with the value set to your app's `GroupIdentifier`. This is necessary to obtain a path for storing the local data warehouse.

6. Modify the `Signing & Capabilities` section in your xcode project as follows:

   ![Signing and capabilities](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt35cd30ea3a66e443/signing_and_capabilities.png)

A sample app that implements this SDK, complete with source code, is available at [https://github.com/webex/webex-ios-sdk-example](https://github.com/webex/webex-ios-sdk-example).



> **Warning**
>
> This example demonstrates how to use the APIs and is not intended for production use.



## Using Swift Package Manager

From WebexSDK `3.17.0` onward, you can integrate the SDK with Swift Package Manager instead of CocoaPods. This requires Xcode 15 or later and an iOS 15 or later deployment target.

1. In Xcode, choose **File > Add Package Dependencies** and enter the package URL:

    ```text
    https://github.com/webex/webex-ios-sdk
    ```

2. Set the dependency rule to **Up to Next Major Version**, starting at `3.17.0`.

3. Add **one** WebexSDK product to your app target. For Webex Calling flows only, add `WebexSDKWxc`, which is equivalent to `pod 'WebexSDK/Wxc'`. For features beyond Webex Calling and for UCM calling, add `WebexSDK`. Whichever product you choose, your code always uses `import WebexSDK`.

4. Complete the same app configuration as the CocoaPods flow: add the `GroupIdentifier` entry to your app's `Info.plist` and configure **Signing & Capabilities** with App Groups.
