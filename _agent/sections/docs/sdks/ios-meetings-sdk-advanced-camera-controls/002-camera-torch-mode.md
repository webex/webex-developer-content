---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/ios-meetings-sdk-advanced-camera-controls
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Camera Torch Mode
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

## Camera Torch Mode

Enable, disable, or auto-enable the camera torch (flashlight). Applicable only to the rear camera:

```swift
var cameraTorchMode: TorchMode
```

![Torch](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt8428c7facee51d39/torch.gif)
