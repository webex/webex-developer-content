---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/android-calling-sdk-additional-methods
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Get an External Tracking ID
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/android-calling-sdk-additional-methods). [Full Markdown](../../../../../docs/sdks/android-calling-sdk-additional-methods.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article describes additional methods available in the Webex Calling Android SDK.

---



> **Info**
>
> The Mobile SDK supports a maximum of two concurrent incoming calls. A third incoming call is automatically ignored or silently dismissed. Only one call can be in a resumed state at any time.

## Selected section

## Get an External Tracking ID

For logging and tracking metrics, use `call.getExternalTrackingId()` to retrieve a tracking ID. This is available in the `onInfoChanged` callback in `CallObserver`.

```kotlin
call.getExternalTrackingId()
// Use the trackingId after the onInfoChanged callback has fired.
```
