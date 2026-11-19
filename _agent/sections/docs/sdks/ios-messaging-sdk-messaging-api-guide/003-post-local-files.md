---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/ios-messaging-sdk-messaging-api-guide
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Post Local Files
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/ios-messaging-sdk-messaging-api-guide). [Full Markdown](../../../../../docs/sdks/ios-messaging-sdk-messaging-api-guide.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article provides detailed information on the messaging features and methods provided by the Webex iOS Messaging SDK.

---

The SDK lets you easily implement real-time messaging capabilities including posting new messages, and deleting, listing, and editing existing messages.

## Selected section

## Post Local Files

To post a message with attached files using local paths:

```swift
let fileItem1 = LocalFile.init(path: "{local file path}")
let fileItem2 = LocalFile.init(path: "{local file path}", name: "{file name}", mime: "{file mime type}")
let fileArray = [fileItem1, fileItem2]

webex.messages.post(roomId: "{room id}", text: "{text...}", files: fileArray){ response in
    switch response.result {
        case .success(let message):
            // ...
            break
        case let .failure(let error):
            // ...
            break
    }
}
```

### Post Files with Uploading Progress

To post a message with a file and monitor the uploading progress:

```swift
guard let fileItem  = LocalFile.init(path: "{local file path}", name: "{file name}", mime: "{file mime type}", 
    progressHandler: { (progress) in // progress as double }) else {return}

webex.messages.post(roomId: "{room id}", text: "{text...}", files: [fileItem]){ response in
    switch response.result {
        case .success(let message):
            // ...
            break
        case let .failure(let error):
            // ...
            break
    }
}
```

### Post Files with a Thumbnail Preview

To post a message with a file that includes a thumbnail:

```swift
let fileThumb = LocalFile.Thumbnail.init(path: "{file path}", mime: "{mime type}", width: 320, height: 400)
guard let fileItem  = LocalFile.init(path: "{local file path}", name: "{file name}", mime: "{file mime type}", 
    thumbnail: fileThumb, progressHandler: { (progress) in // progress as double }) else {return}

webex.messages.post(roomId: "{room id}", text: "{text...}", files: [fileItem]){ response in
    switch response.result {
        case .success(let message):
            // ...
            break
        case let .failure(let err):
            // ...
            break
    }
}
```
