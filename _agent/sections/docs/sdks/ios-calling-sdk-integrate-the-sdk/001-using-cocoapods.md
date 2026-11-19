---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/ios-calling-sdk-integrate-the-sdk
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Using CocoaPods
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/ios-calling-sdk-integrate-the-sdk). [Full Markdown](../../../../../docs/sdks/ios-calling-sdk-integrate-the-sdk.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

You can integrate the Webex iOS SDK into your app using either [CocoaPods](https://guides.cocoapods.org/using/getting-started.html) or Swift Package Manager.

## Selected section

## Using CocoaPods



> **Warning**
>
> On December 2, 2026, CocoaPods trunk will stop accepting new pod versions. Existing CocoaPods integrations will keep working, but you must use Swift Package Manager to get later Webex iOS SDK releases. See the [CocoaPods trunk read-only plan](https://blog.cocoapods.org/CocoaPods-Specs-Repo/).





> **Info**
>
> Swift Package Manager is supported from WebexSDK 3.17.0 onward. Both channels deliver the same binaries. For Swift Package Manager, see [Using Swift Package Manager](https://developer.webex.com/docs/sdks/ios-calling-sdk-integrate-the-sdk#using-swift-package-manager).



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
