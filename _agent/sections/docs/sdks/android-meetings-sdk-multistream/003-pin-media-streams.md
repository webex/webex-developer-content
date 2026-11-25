---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/android-meetings-sdk-multistream
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Pin Media Streams
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

## Pin Media Streams

Pin a participant's stream to prevent it from changing, regardless of their speaking or queue status.

- The pinning feature falls under Category-C APIs.
- Pinned streams do not enter the active speaker stage.



> **Info**
>
> The pinning feature is part of the Category-C APIs, available from SDK version 3.6.0 onwards.



![Pin a stream](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt63d6386d299a09fc/multiStream_pinstream.png)

### Pin or Update a Pinned Stream

To pin or update a pinned stream for a specific participant:

```kotlin
fun setMediaStreamCategoryC(participantId: String, quality: MediaStreamQuality)
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

### Unpin a Media Stream

To unpin a participant's stream:

```kotlin
fun removeMediaStreamCategoryC(participantId: String)
```

### Check for Pinning Support

To determine if stream pinning is supported:

```kotlin
fun isMediaStreamsPinningSupported() : Boolean
```

### Listen for Media Stream Changes

To listen for changes in media stream properties, register a change listener to handle events:

```kotlin
enum class MediaStreamChangeEventType {
    Size,
    Membership,
    Video,
    Audio,
    PinState
}
```

```kotlin
fun setOnMediaStreamInfoChanged(listener: (type: MediaStreamChangeEventType, info: MediaStreamChangeEventInfo) -> Unit)
```
