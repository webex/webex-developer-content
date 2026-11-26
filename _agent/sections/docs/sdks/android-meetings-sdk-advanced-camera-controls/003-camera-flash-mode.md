---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/android-meetings-sdk-advanced-camera-controls
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Camera Flash Mode
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/android-meetings-sdk-advanced-camera-controls). [Full Markdown](../../../../../docs/sdks/android-meetings-sdk-advanced-camera-controls.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

The Android Meetings SDK provides methods that let you have enhanced control over the device's system camera. Users can adjust exposure values, set the zoom factor, manage the camera torch, and more.

---



> **Info**
>
> Available starting from SDK version 3.3.0 and later.

## Selected section

## Camera Flash Mode

Control the camera flash that activates during the `takePhoto()` method call:

```kotlin
setCameraFlashMode(mode: FlashMode)
```

![Control the flash](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt2849f9b986d2c503/flash_takephoto.gif)
