---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/ios-meetings-sdk-multistream
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Implement Multistream
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/ios-meetings-sdk-multistream). [Full Markdown](../../../../../docs/sdks/ios-meetings-sdk-multistream.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

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
- Use the [Active Speaker Method](https://webex.github.io/webex-ios-sdk/Structs/CallMembership.html#/s:8WebexSDK14CallMembershipV15isActiveSpeakerSbvp) to determine active speakers.
- The [ActiveSpeakerChangedEvent](https://webex.github.io/webex-ios-sdk/Classes/Call/MediaChangedEvent.html#/s:8WebexSDK4CallC17MediaChangedEventO013activeSpeakereF0yAeA0C10MembershipVSg_AItcAEmF) is triggered when the active speaker changes.

![Multistream](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt1f4e2f758de3738d/multiStreamNew.png)

## Selected section

## Implement Multistream

Register the `onMediaStreamAvailabilityListener` callback to manage stream availability:

```swift
call.onMediaStreamAvailabilityListener = { available, stream in 
    // if available {
    //     // new stream available
    //} else {
    //     // stream unavailable
    //}
}
```

### 1. Render a New Stream

When a new stream becomes available, provide a view for the SDK to render the video:

```swift
// MediaStream object returned by callback
let view = MediaRenderView()
stream.renderView = view
```

### 2. Implement a Media Stream Information Change Listener

Different `MediaStreamChangeEventType` values are supported. Events are triggered when related changes occur:

```swift
enum MediaStreamChangeEventType {
    case Size
    case Membership
    case Video
    case Audio
}
```

Register an info change listener to receive updates:

```swift
// stream is MediaStream object returned by onMediaStreamAvailabilityListener callback 
stream.setOnMediaStreamInfoChanged { type, info in
    // type: MediaStreamChangeEventType
    // info: MediaStreamChangeEventInfo
}
```

### 3. Configure Media Stream for Category-A

Category-A contains a single active speaker stream. Add or update this stream with the specified parameters:

```swift
// Duplicate if true; the same active speaker will also be included in Category-B streams.
fun setMediaStreamCategoryA(duplicate: Boolean, quality: MediaStreamQuality)
```

Define the video quality:

```swift
enum MediaStreamQuality {
    case Undefined
    case LD  // 180p
    case SD  // 360p
    case HD  // 720p
    case FHD // 1080p
}
```

### 4. Adjust Media Streams for Category-B

Set parameters for all Category-B streams:

- If the number of existing B streams is less than `numStreams`, additional B streams will be added as necessary.
- If the number of existing B streams is more than `numStreams`, the extra B streams will be removed.

```swift
fun setMediaStreamsCategoryB(numStreams: Int, quality: MediaStreamQuality)
```

### 5. Remove Media Stream from Category-A

Remove the active speaker stream from Category-A:

```swift
fun removeMediaStreamCategoryA()
```

After removal, if Category-B exists, all streams have equal priority, and no changes occur based on speaking activity.

### 6. Remove Media Streams from Category-B

To clear all Category-B streams:

```swift
fun removeMediaStreamsCategoryB()
```

After clearing the Category-B streams, if Category-A remains, only the active speaker's stream is visible.
