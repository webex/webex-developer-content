---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/ios-calling-sdk-integrate-the-sdk
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Using Swift Package Manager
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/ios-calling-sdk-integrate-the-sdk). [Full Markdown](../../../../../docs/sdks/ios-calling-sdk-integrate-the-sdk.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

You can integrate the Webex iOS SDK into your app using either [CocoaPods](https://guides.cocoapods.org/using/getting-started.html) or Swift Package Manager.

## Selected section

## Using Swift Package Manager

From WebexSDK `3.17.0` onward, you can integrate the SDK with Swift Package Manager instead of CocoaPods. This requires Xcode 15 or later and an iOS 15 or later deployment target.

1. In Xcode, choose **File > Add Package Dependencies** and enter the package URL:

    ```text
    https://github.com/webex/webex-ios-sdk
    ```

2. Set the dependency rule to **Up to Next Major Version**, starting at `3.17.0`.

3. Add **one** WebexSDK product to your app target. For Webex Calling flows only, add `WebexSDKWxc`, which is equivalent to `pod 'WebexSDK/Wxc'`. For features beyond Webex Calling and for UCM calling, add `WebexSDK`. Whichever product you choose, your code always uses `import WebexSDK`.

4. Complete the same app configuration as the CocoaPods flow: add the `GroupIdentifier` entry to your app's `Info.plist` and configure **Signing & Capabilities** with App Groups.
