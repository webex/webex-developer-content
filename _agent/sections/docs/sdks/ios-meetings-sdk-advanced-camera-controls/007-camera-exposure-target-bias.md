---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/ios-meetings-sdk-advanced-camera-controls
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Camera Exposure Target Bias
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

## Camera Exposure Target Bias

Get the minimum, maximum, and current values of the camera's target bias. Default is 0 until set:

```swift
var exposureTargetBias: CameraExposureTargetBias
```
