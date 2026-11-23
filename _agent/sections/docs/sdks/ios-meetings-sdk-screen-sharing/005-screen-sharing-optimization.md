---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/ios-meetings-sdk-screen-sharing
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Screen Sharing Optimization
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/ios-meetings-sdk-screen-sharing). [Full Markdown](../../../../../docs/sdks/ios-meetings-sdk-screen-sharing.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

The Webex iOS Meetings SDK allows you to share the entire screen of your iOS mobile device during a call or meeting.

---

This article guides your through implementing screen sharing in your own iOS application.

## Selected section

## Screen Sharing Optimization

The ScreenShare Optimization methods can enhance screen sharing for video and text. These improvements are available from version 3.9.0 onwards.

### Screen Sharing Optimization Examples

Screen sharing methods are accessible through the `Call` object. The `Call` object can be obtained as a result of the `webex.phone.dial` method or through the `webex.phone.onIncoming` method for an incoming call:

1. Start ScreenSharing with `shareConfig`:

    ```swift
    call.startSharing(shareConfig: self.shareConfig, completionHandler: { error in
        if error != nil {
            print("share screen error:\(String(describing: error))")
        }
    })
    ```

    The `shareConfig` parameter is optional. If not provided, the default optimization will apply, and audio will not be shared. This parameter was introduced in version 3.9.0.

2. Retrieve the active sharing type for the current call with the `getShareConfig` method.

    ```swift
    let sharingConfig = call.getShareConfig()
    ```

### Set ShareConfig

To configure `ShareConfig`:

```swift
    // This doesn't set any special optimization. Maximum is 3 fps. This is the default setting if no parameters are passed to the shareConfig param.
    let shareConfig = ShareConfig(ShareOptimizeType.Default, false)

    // This helps in optimizing screenshare while sharing video and motion without audio. Maximum is 30 fps.
    let shareConfig = ShareConfig(ShareOptimizeType.OptimizeVideo, false)

    // This helps in optimizing screenshare while sharing text and images. Maximum is 3 fps. Resolution of text and images gets better.
    let shareConfig = ShareConfig(ShareOptimizeType.OptimizeText, false)
```

### Configure OptimizeVideo in BroadcastExtension

When a user selects `ShareOptimizeType.OptimizeVideo`, communicate this choice to the `BroadcastExtension` using `UserDefaults`:

```swift
if let defaults = UserDefaults(suiteName: groupIdentifier)
{
    switch self.shareConfig?.shareType {
    case .OptimizeVideo:
        defaults.setValue(true, forKey: "optimizeForVideo")
    default:
        defaults.setValue(false, forKey: "optimizeForVideo")
    }
}
```

Based on this setting, call the appropriate method in `WebexBroadcastExtension`:

```swift
if UserDefaults(suiteName: groupIdentifier)?.bool(forKey: "optimizeForVideo") == true {
    WebexBroadcastExtension.sharedInstance.optimizeForVideo()
}
```
