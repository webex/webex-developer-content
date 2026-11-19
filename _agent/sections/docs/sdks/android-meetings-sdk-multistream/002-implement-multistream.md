---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/android-meetings-sdk-multistream
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Implement Multistream
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/android-meetings-sdk-multistream). [Full Markdown](../../../../../docs/sdks/android-meetings-sdk-multistream.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Multistream enhances meeting experiences by showcasing the most active participants' videos.

---

The following features have been introduced in SDK version 3.5.0 and later:

- Streams are ordered by participant join time.
- There are two categories: Category-A and Category-B.
- Category-A contains only the active speaker's stream.
- Category-B includes all other streams and may also contain the active speaker's stream as a duplicate.
- The number of streams in Category-B can be limited; additional participants are queued.
- Queued participants replace less active streams when they speak.
- When a stream participant leaves, a random queued participant takes their place.
- Use the [Active Speaker API](https://webex.github.io/webex-android-sdk/com.ciscowebex.androidsdk.phone/-call-membership/is-active-speaker.html) to determine active speakers.
- The [ActiveSpeakerChangedEvent](https://webex.github.io/webex-android-sdk/com.ciscowebex.androidsdk.phone/-call-observer/-active-speaker-changed-event/index.html) is activated when the active speaker changes.

![Multistream example](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltad82d3ce7eb9750f/multiStreamNew.png)

## Selected section

## Implement Multistream

Clients should implement `MediaStreamAvailabilityEvent` as part of `CallObserver.onMediaChanged`:

```kotlin
override fun onMediaChanged(event: CallObserver.MediaChangedEvent?) {
     event?.let { _event ->
            val call = _event.getCall()
            when (_event) {
                is CallObserver.MediaStreamAvailabilityEvent -> {
                    // event is CallObserver.MediaStreamAvailabilityEvent
                    //if (event.isAvailable()) {
                    //     new stream available
                    //} else {
                    //     stream unavailable
                    //}
                }
                else -> {}
            }
}
```

### Render a New Stream

Provide a view to render newly available streams, such as when new participants join:

```kotlin
// event is CallObserver.MediaStreamAvailabilityEvent
event.getStream()?.setRenderView(view)
```

### Media Stream Information Changes

Different `MediaStreamChangeEventType` are supported. Events trigger when related changes occur:

```kotlin
enum class MediaStreamChangeEventType {
    Size,
    Membership,
    Video,
    Audio
}
```

Register an info change listener to receive updates:

```kotlin
// event is CallObserver.MediaStreamAvailabilityEvent
event.getStream()?.setOnMediaStreamInfoChanged { type, info ->
                    //type: MediaStreamChangeEventType
                    //info: MediaStreamChangeEventInfo
                }
```

### Set a Media Stream for Category-A

Add or update the active speaker stream in Category-A, which contains only one stream:

```kotlin
// duplicate if true, the same active speaker will also be included in Category-B streams.
fun setMediaStreamCategoryA(duplicate: Boolean, quality: MediaStreamQuality)
```

```kotlin
enum class MediaStreamQuality {
    Undefined,
    LD,  // 180p
    SD,  // 360p
    HD,  // 720p
    FHD // 1080p
}
```

### Set Media Streams for Category-B

Adjust the number and quality of Category-B streams:

- If the number of existing B streams is less than `numStreams`, it will add B streams as necessary.
- If the number of existing B streams is more than `numStreams`, it will remove the extra B streams.

```kotlin
fun setMediaStreamsCategoryB(numStreams: Int, quality: MediaStreamQuality)
```

### Remove a Media Stream from Category-A

Remove the active speaker stream from Category-A:

```kotlin
fun removeMediaStreamCategoryA()
```

After the removal of Category-A, if Category-B exists, all streams will have the same priority, and streams will not change based on the active speaker.

### Remove Media Streams from Category-B

Remove all streams from Category-B:

```kotlin
fun removeMediaStreamsCategoryB()
```
