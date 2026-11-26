---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/ios-messaging-sdk-messaging-api-guide
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- List Messages Before a Specific Date
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/ios-messaging-sdk-messaging-api-guide). [Full Markdown](../../../../../docs/sdks/ios-messaging-sdk-messaging-api-guide.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article provides detailed information on the messaging features and methods provided by the Webex iOS Messaging SDK.

---

The SDK lets you easily implement real-time messaging capabilities including posting new messages, and deleting, listing, and editing existing messages.

## Selected section

## List Messages Before a Specific Date

To list messages before a particular date point within a room, with `max` specifying the maximum number of messages to return:

```swift
let before = Before.date("{one date point}")

webex.messages.list(roomId: "{room id}", before: before, max: 50) { response in
    switch response.result {
    case .success(let messages):
        // ...
        break
    case .failure(let err):
        // ...
        break
    }
}
```
