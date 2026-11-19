---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/ios-meetings-sdk-advanced-camera-controls
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Take a Photo
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/ios-meetings-sdk-advanced-camera-controls). [Full Markdown](../../../../../docs/sdks/ios-meetings-sdk-advanced-camera-controls.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

The iOS Meetings SDK provides methods that let you have enhanced control over the device's system camera. Users can adjust exposure values, set the zoom factor, manage the camera torch, and more.

---



> **Info**
>
> Available starting from SDK version 3.3.0 and later.

## Selected section

## Take a Photo

Capture a photo from the local view. The photo data is returned as a byte array:

```swift
func takePhoto() -> Bool
```

```swift
Call.onPhotoCaptured: ((_ imageData: Data?) -> Void)?
```

![Take a Photo](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltf54c07a53d1b6e6f/takephoto.gif)
