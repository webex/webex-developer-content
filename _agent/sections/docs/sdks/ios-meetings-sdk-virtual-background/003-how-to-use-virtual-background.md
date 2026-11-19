---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/ios-meetings-sdk-virtual-background
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- How to Use Virtual Background
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/ios-meetings-sdk-virtual-background). [Full Markdown](../../../../../docs/sdks/ios-meetings-sdk-virtual-background.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Enhance your video appearance and maintain professionalism, privacy, and focus by using a virtual background in meetings.

---

This article describes how you can use the Webex iOS Meetings SDK to work with virtual backgrounds in your app.

## Selected section

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
