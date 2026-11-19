---
type: Guide
title: Android Meetings SDK | Virtual Background
display_title: Virtual Background
canonical_url: https://developer.webex.com/docs/sdks/android-meetings-sdk-virtual-background
content_type: documentation
product_group:
- webex-suite
categories:
- meeting
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/android-meetings-sdk-virtual-background)

Enhance your video appearance and maintain professionalism, privacy, and focus by using a virtual background in meetings.

---

This article describes how you can use the Webex Android Meetings SDK to work with virtual backgrounds in your app.

## Virtual Background Notes

When using custom virtual backgrounds, consider the following guidelines:

- Supported image formats for custom backgrounds are JPG and PNG.
- The SDK resizes images larger than 1280x720 to avoid excessive CPU usage.
- Application storage will increase based on the custom images used.
- High CPU usage by the Virtual Background feature may trigger `CallObserver.onCpuHitThreshold()`. If that happens, consider disabling the feature.

## Virtual Background Types

The Webex iOS Meetings SDK lets you choose from three options:

- None
- Blur
- Custom

### None

Removes any custom or blurred background, effectively disabling the virtual background feature. This is the default setting.

![None](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt7751d29d8b43b7ad/vbg_normal.png)

### Blur

Applies a blur effect to the background.

![Blur](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt6760b3aab990b22c/vbg_blur.png)

### Custom

Allows the use of a personal image as the background.

![Custom Virtual Background](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt3381bf0302342cf3/vbg_custom.png)

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
