---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/android-meetings-sdk-virtual-background
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- How to Use Virtual Backgrounds
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/android-meetings-sdk-virtual-background). [Full Markdown](../../../../../docs/sdks/android-meetings-sdk-virtual-background.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Enhance your video appearance and maintain professionalism, privacy, and focus by using a virtual background in meetings.

---

This article describes how you can use the Webex Android Meetings SDK to work with virtual backgrounds in your app.

## Selected section

## How to Use Virtual Backgrounds

The following sections describe how to use the virtual background functionality in the Webex iOS Meetings SDK.

### Check Device Compatibility

To check if the device supports virtual backgrounds:

```kotlin
val isSupported: Boolean = webex.phone.isVirtualBackgroundSupported()
```

### Fetch Available Virtual Backgrounds

To retrieve available virtual backgrounds:

```kotlin
webex.phone.fetchVirtualBackgrounds( CompletionHandler { result ->  
    if (result.isSuccessful) {
        val data: List<VirtualBackground>? = result.data
        //display the background
    } else {
        Log.d(tag, "error: ${result.error?.message}")
    }
})
```

### Upload a Custom Virtual Background

To upload a custom virtual background:

```kotlin
val thumbnailFile = FileUtils.getFileFromResource(this, "nature-thumb")
val file = FileUtils.getFileFromResource(this, "nature")
val thumbnail = LocalFile.Thumbnail(thumbnailFile, null, 64, 64)

val imgFile = LocalFile(file, null, thumbnail, null)

webex.phone.addVirtualBackground(imgFile, CompletionHandler { result ->
    if (result.isSuccessful) {
        val data: VirtualBackground? = result.data
        //handle the success response
    } else {
        Log.d(tag, "error: ${result.error?.message}")
    }
})
```

### Apply a Virtual Background

To apply a virtual background:

```kotlin
//Specify the mode PREVIEW or CALL as per requirement. 
val mode = Phone.VirtualBackgroundMode.PREVIEW // Phone.VirtualBackgroundMode.CALL
webex.phone.applyVirtualBackground(virtualBackgroundItem, mode, CompletionHandler { result ->
    if (result.isSuccessful) {
        val data: Boolean? = result.data
        //handle the success response
    } else {
            Log.d(tag, "error: ${result.error?.message}")
    }
})
```

Specify the display mode, set either `PREVIEW` or `CALL`, depending on your requirements.

### Remove Virtual Background

To remove a virtual background:

```kotlin
webex.phone.removeVirtualBackground(background, CompletionHandler { result ->
    if (result.isSuccessful) {
        val data: Boolean? = result.data
        //handle the delete response
    } else {
        Log.d(tag, "error: ${result.error?.message}")
    }
})
```

### Manage the Virtual Background Limit

Set the number of virtual backgrounds that you want to support. The default limit is 3.

```kotlin
webex.phone.setMaxVirtualBackgroundItems(limit)
```

### Retrieve the Background Limit

To retrieve the current virtual background limit:

```kotlin
val limit: Int = webex.phone.getMaxVirtualBackgroundItems()
```
