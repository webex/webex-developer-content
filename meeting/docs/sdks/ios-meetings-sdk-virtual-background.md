---
type: Guide
title: iOS Meetings SDK | Virtual Background
display_title: Virtual Background
canonical_url: https://developer.webex.com/docs/sdks/ios-meetings-sdk-virtual-background
content_type: documentation
product_group:
- webex-suite
categories:
- meeting
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/ios-meetings-sdk-virtual-background)

Enhance your video appearance and maintain professionalism, privacy, and focus by using a virtual background in meetings.

---

This article describes how you can use the Webex iOS Meetings SDK to work with virtual backgrounds in your app.

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

Removes any custom or blurred background, effectively disabling the virtual background feature. This is the default setting:

![None](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltb39ea3bdf8fc08f3/NoneVB.png)

### Blur

Applies a blur effect to the background.

![Blur](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt487dec2b4f923640/BlurVB.png)

### Custom

Allows the use of a personal image as the background.

![Custom Virtual Background](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt150a6a34563304d2/CustomVB.png)

## How to Use Virtual Background

The following sections describe how to use the virtual background functionality in the Webex iOS Meetings SDK.

### Check Device Compatibility

To check if the device supports virtual backgrounds:

```swift
isVirtualBackgroundSupported: Bool
```

### Fetch Available Virtual Backgrounds

To retrieve available virtual backgrounds:

```swift
fetchVirtualBackgrounds(completionHandler: @escaping (_ result: Result<[VirtualBackground]>) -> Void)
```

### Upload a Custom Virtual Background

To upload a custom virtual background:

```swift
func addVirtualBackground(image: LocalFile, completionHandler: @escaping (_ result: Result<VirtualBackground>) -> Void)
```

### Apply Virtual Background

To apply a virtual background:

```swift
func applyVirtualBackground(background: VirtualBackground, mode: VirtualBackgroundMode, completionHandler: @escaping (_ result: Result<Bool>) -> Void)
```

Specify the display mode, set either `preview` or `call`, depending on your requirements.

### Remove Virtual Background

To remove a virtual background:

```swift
func removeVirtualBackground(background: VirtualBackground, completionHandler: @escaping (_ result: Result<Bool>) -> Void)
```

### Manage Virtual Background Limit

Set the number of virtual backgrounds that you want to support. The default limit is 3.

```swift
var virtualBackgroundLimit: Int
```
