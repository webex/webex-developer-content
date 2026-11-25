---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/android-messaging-sdk-features-and-methods
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Download Thumbnail Images
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/android-messaging-sdk-features-and-methods). [Full Markdown](../../../../../docs/sdks/android-messaging-sdk-features-and-methods.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article provides detailed information on the messaging features and methods provided by the Webex Android Messaging SDK.

---

The SDK lets you easily implement real-time messaging capabilities including posting new messages, and deleting, listing, and editing existing messages.

## Selected section

## Download Thumbnail Images

To download thumbnail images associated with a `RemoteFile` object:

`file` is the local file directory in which the thumbnail is to be saved.
```kotlin
webex.messages.downloadThumbnail(remoteFile, file, CompletionHandler { result ->
    if (result.isSuccessful) {
        if (result.data != null) {
            // result.data gives the thumbnail URI
        } else {
            // Error occurred
        }
    } else {
        emitter.onError(Throwable(result.error?.errorMessage))
    }
})
```



> **Info**
>
> The `remoteFile` is the target file and is of type [Remote File](https://webex.github.io/webex-android-sdk/-s-d-k/com.ciscowebex.androidsdk.message/-remote-file/index.html?query=interface%20RemoteFile).
