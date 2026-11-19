---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/ios-messaging-sdk-messaging-api-guide
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Download Files with a Progress Handler
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/ios-messaging-sdk-messaging-api-guide). [Full Markdown](../../../../../docs/sdks/ios-messaging-sdk-messaging-api-guide.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article provides detailed information on the messaging features and methods provided by the Webex iOS Messaging SDK.

---

The SDK lets you easily implement real-time messaging capabilities including posting new messages, and deleting, listing, and editing existing messages.

## Selected section

## Download Files with a Progress Handler

In addition to downloading the files, this snippet provides a progress handler that reports the progress of the file download:

```swift
webex.messages.onEvent = { messageEvent in
    switch messageEvent{
    case .messageReceived(let message):
        if let files = message.files {
            for file in files {
               webex.messages.downloadFile(file, progressHandler: { progress in
                      // progress in double
               }) { result in
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
