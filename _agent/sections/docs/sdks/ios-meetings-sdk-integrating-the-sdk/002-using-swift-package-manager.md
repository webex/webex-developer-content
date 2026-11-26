---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/ios-meetings-sdk-integrating-the-sdk
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Using Swift Package Manager
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/ios-meetings-sdk-integrating-the-sdk). [Full Markdown](../../../../../docs/sdks/ios-meetings-sdk-integrating-the-sdk.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

You can integrate the Webex iOS SDK into your app using either CocoaPods or Swift Package Manager.

## Selected section

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
