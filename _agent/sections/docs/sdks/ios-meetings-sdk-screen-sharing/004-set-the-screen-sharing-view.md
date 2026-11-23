---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/ios-meetings-sdk-screen-sharing
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Set the Screen Sharing View
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/ios-meetings-sdk-screen-sharing). [Full Markdown](../../../../../docs/sdks/ios-meetings-sdk-screen-sharing.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

The Webex iOS Meetings SDK allows you to share the entire screen of your iOS mobile device during a call or meeting.

---

This article guides your through implementing screen sharing in your own iOS application.

## Selected section

## Set the Screen Sharing View

Use [`MediaOption`](https://webex.github.io/webex-ios-sdk/Structs/MediaOption.html) to configure the viewing of shared screens from remote participants.

```swift
let option = MediaOption.audioVideoScreenShare(video: (localVideoView, remoteVideoView), screenShare: remoteScreenView)

webex.phone.dial("coworker@acm.com", option: option) { ret in
    switch ret {
    case .success(let call):
        call.onConnected = {
            // ...
        }
        call.onDisconnected = { reason in
            // ...
        }
    case .failure(let error):
        // Failure.
    }
}
```

Provide a view only when the other party starts sharing their screen:

```swift
let option = MediaOption.audioVideoScreenShare(video: (localVideoView, remoteVideoView))

webex.phone.dial("coworker@acm.com", option: option) { ret in
    switch ret {
    case .success(let call):
        call.onConnected = {
            // ...
        }
        call.onDisconnected = { reason in
            // ...
        }
        call.onMediaChanged = { changed in
            switch changed {
                ...
            case .remoteSendingScreenShare(let sending):
                call.screenShareRenderView = sending ? remoteScreenView : nil
            }
        }
    case .failure(let error):
        // failure
    }
}
```
