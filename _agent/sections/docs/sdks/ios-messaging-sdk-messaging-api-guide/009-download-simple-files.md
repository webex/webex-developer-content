---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/ios-messaging-sdk-messaging-api-guide
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Download Simple Files
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/ios-messaging-sdk-messaging-api-guide). [Full Markdown](../../../../../docs/sdks/ios-messaging-sdk-messaging-api-guide.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article provides detailed information on the messaging features and methods provided by the Webex iOS Messaging SDK.

---

The SDK lets you easily implement real-time messaging capabilities including posting new messages, and deleting, listing, and editing existing messages.

## Selected section

## Download Simple Files

When a message with files is received, this code will download each file to default location:

```swift
webex.messages.onEvent = { messageEvent in
    switch messageEvent{
    case .messageReceived(let message):
        if let files = message.files {
            for file in files {
                webex.messages.downloadFile(file) { result in
                    if let localUrl = result.data{
                        // file downloaded successfully in localUrl ...
                    }
                }
            }
        }
        break
    case .messageDeleted(let messageId):
        // ...
        break
    }
}
```
