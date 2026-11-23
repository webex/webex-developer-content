---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/android-meetings-sdk-advanced-camera-controls
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Camera Focus at Point
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

## Camera Focus at Point

Focus the camera at a specific X and Y coordinate:

```kotlin
setCameraFocusAtPoint(pointX: Float, pointY: Float)
```
