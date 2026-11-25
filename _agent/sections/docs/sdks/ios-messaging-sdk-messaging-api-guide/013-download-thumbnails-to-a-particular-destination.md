---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/ios-messaging-sdk-messaging-api-guide
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Download Thumbnails to a Particular Destination
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/ios-messaging-sdk-messaging-api-guide). [Full Markdown](../../../../../docs/sdks/ios-messaging-sdk-messaging-api-guide.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article provides detailed information on the messaging features and methods provided by the Webex iOS Messaging SDK.

---

The SDK lets you easily implement real-time messaging capabilities including posting new messages, and deleting, listing, and editing existing messages.

## Selected section

## Download Thumbnails to a Particular Destination

Similar to downloading files, this snippet specifies a destination for the downloaded thumbnails:

```swift
webex.messages.onEvent = { messageEvent in
    switch messageEvent{
    case .messageReceived(let message):
        let destination = URL.init(string: "{destination directory}")
        if let files = message.files {
            for file in files {
               webex.messages.downloadThumbnail(for: file, to: destination) { result in
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
