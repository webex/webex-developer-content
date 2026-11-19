---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/ios-messaging-sdk-messaging-api-guide
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Get Space Read Status
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/ios-messaging-sdk-messaging-api-guide). [Full Markdown](../../../../../docs/sdks/ios-messaging-sdk-messaging-api-guide.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article provides detailed information on the messaging features and methods provided by the Webex iOS Messaging SDK.

---

The SDK lets you easily implement real-time messaging capabilities including posting new messages, and deleting, listing, and editing existing messages.

## Selected section

## Get Space Read Status

To get the read status of a space for the logged-in user:

```swift
webex.spaces.getWithReadStatus(spaceId: spaceId, completionHandler: { response in
      switch response.result {
      case .success(let spaceInfo):
          if let lastActivityDate = spaceInfo.lastActivityDate,
              let lastSeenDate = spaceInfo.lastSeenActivityDate,
              lastActivityDate > lastSeenDate {
              // Space has unread messages.
          } else {
              // Space is fully read.
          }
      case .failure(let error):
          // Handle error.
      }
})
```
