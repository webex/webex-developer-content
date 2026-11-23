---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/android-meetings-sdk-multistream-legacy-support
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Implementing Multistream in SDK 3.0
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/android-meetings-sdk-multistream-legacy-support). [Full Markdown](../../../../../docs/sdks/android-meetings-sdk-multistream-legacy-support.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article provides details on how to use multistream features in older versions of the Webex Mobile SDK.

---

However, we highly recommend using the latest Webex Mobile SDKs. Refer to the newer [Multistream](https://developer.webex.com/docs/sdks/android-meetings-sdk-multistream) documentation for the current implementation.

## Selected section

## Implementing Multistream in SDK 3.0

To implement multi-stream in SDK 3.0, inherit from `MultiStreamObserver`:

```kotlin
interface MultiStreamObserver {
    fun onAuxStreamAvailable(): View?
    fun onAuxStreamUnavailable(): View?
    fun onAuxStreamChanged(event: AuxStreamChangedEvent?)
}
```

### Provide a View to Open a Stream

When a new stream is available, the `onAuxStreamAvailable` method is called. The client provides a view to render the stream:

```kotlin
override fun onAuxStreamAvailable(): View? {
    return mediaRenderView
}
```

### Provide a View to Close the Stream

If a stream is unavailable, such as when a participant leaves the meeting and the number of joined participants is smaller than the number of opened streams, the SDK will trigger the `OnAuxStreamUnavailable` callback. The client should provide the SDK with a view handle to be closed. If the given view is null, the SDK will automatically close the last opened stream if needed:

```kotlin
override fun onAuxStreamUnavailable(): View? {
    return null
}
```

### Display the Stream View

Handle the `AuxStreamOpenedEvent` to display the stream view when it is successfully opened.

### Hide the Stream View

Handle the `AuxStreamClosedEvent` to hide the stream view when it is successfully closed:

```kotlin
override fun onAuxStreamChanged(event: MultiStreamObserver.AuxStreamChangedEvent?) {
    val auxStream: AuxStream? = event?.getAuxStream()

    when (event) {
        is MultiStreamObserver.AuxStreamOpenedEvent -> {
            if (event.isSuccessful()) {
                ...
            } else {
                // error occurred
            }
        }
        is MultiStreamObserver.AuxStreamClosedEvent -> {
            if (event.isSuccessful()) {
                ...
            } else {
                // error occurred
            }
        }
        is MultiStreamObserver.AuxStreamSendingVideoEvent -> {
            ...     
        }
        is MultiStreamObserver.AuxStreamPersonChangedEvent -> {
            ...
        }
        is MultiStreamObserver.AuxStreamSizeChangedEvent -> {
            ...
        }
    }
}
```
