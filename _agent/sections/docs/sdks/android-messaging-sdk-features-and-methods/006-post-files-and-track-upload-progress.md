---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/android-messaging-sdk-features-and-methods
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Post Files and Track Upload Progress
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/android-messaging-sdk-features-and-methods). [Full Markdown](../../../../../docs/sdks/android-messaging-sdk-features-and-methods.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article provides detailed information on the messaging features and methods provided by the Webex Android Messaging SDK.

---

The SDK lets you easily implement real-time messaging capabilities including posting new messages, and deleting, listing, and editing existing messages.

## Selected section

## Post Files and Track Upload Progress

To attach files to messages:

```kotlin
// Attach files to a message
val text = Message.Text.plain("hello world")
// Create a File object
val tempFile = File.createTempFile("tempFile", ".txt")
// Create a local file object
val localFile = LocalFile(tempFile, "text/html", null, null)
val listOfFiles = ArrayList<LocalFile>()
listOfFiles.add(localFile)
webex.messages.postToSpace(spaceId, text, mentionsList, listOfFiles, completionHandler)
```

To track the file upload progress:

```kotlin
// Track upload progress

val text = Message.Text.plain("hello world")
// Create a File object
val tempFile = File.createTempFile("tempFile", ".txt")
// Create a local file object
val localFile = LocalFile(tempFile, "text/html", null, object : MessageClient.ProgressHandler {
    override fun onProgress(bytes: Double) {
        // Use the bytes value to denote quantity uploaded
    }
})
val listOfFiles = ArrayList<LocalFile>()
listOfFiles.add(localFile)
webex.messages.postToSpace(spaceId, text, mentionsList, listOfFiles, completionHandler)
```
