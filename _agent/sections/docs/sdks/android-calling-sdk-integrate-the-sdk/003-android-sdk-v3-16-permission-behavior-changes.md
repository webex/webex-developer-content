---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/android-calling-sdk-integrate-the-sdk
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Android SDK v3.16+ Permission Behavior Changes
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/android-calling-sdk-integrate-the-sdk). [Full Markdown](../../../../../docs/sdks/android-calling-sdk-integrate-the-sdk.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

The Webex Android SDK is available through Maven. Follow the instructions below to integrate the SDK into your application.

## Selected section

## Android SDK v3.16+ Permission Behavior Changes

From Android SDK v3.16 onwards, runtime permission handling is app-owned:

* The SDK does not include dangerous permissions in the library manifest.
* The SDK does not show permission dialogs.
* Your app must declare required permissions and request them at runtime before SDK operations.
* If permissions are missing, SDK APIs return `WebexError.ErrorCode.PERMISSION_REQUIRED` and include missing permissions in `error.data`.

The SDK also includes support for 16 KB memory page size on Android; no app code change is required for that part.

### Common calling permissions

```xml
<uses-permission android:name="android.permission.RECORD_AUDIO" />
<uses-permission android:name="android.permission.CAMERA" />
```

### Runtime permission check example

```kotlin
val required = listOf(Manifest.permission.RECORD_AUDIO)
val missing = required.filter {
    ContextCompat.checkSelfPermission(ctx, it) != PackageManager.PERMISSION_GRANTED
}

if (missing.isNotEmpty()) {
    // requestPermissions(missing.toTypedArray(), REQ_CODE)
    return
}

webex.phone.dial(address, MediaOption.audioOnly()) { result ->
    // Handle result. If permission is missing, SDK returns PERMISSION_REQUIRED.
}
```
