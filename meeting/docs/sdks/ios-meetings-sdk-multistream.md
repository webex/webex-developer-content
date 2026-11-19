---
type: Guide
title: iOS Meetings SDK | Multistream
display_title: Multistream
canonical_url: https://developer.webex.com/docs/sdks/ios-meetings-sdk-multistream
content_type: documentation
product_group:
- webex-suite
categories:
- meeting
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/ios-meetings-sdk-multistream)

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

## Common Use Case

For meetings with more than two participants, multistream can display the active speaker and other attendees simultaneously.

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

## Pin Participant Streams

The pin stream feature ensures a participant's video remains visible regardless of their speaking status or queue position.



> **Info**
>
> The pinning methods were introduced in SDK version 3.6.0 and fall under Category-C methods.



![Multistream Pin Stream](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt5c0db64dcddd8bad/multiStream_pinstream.png)

### Typical Scenario

Multistream pinning allows you to pin a participant's stream while viewing the active speaker and other attendees in a multi-participant meeting.

### 1. Pin or Update a Pinned Participant Stream

To pin or update a pinned participant stream:

```swift
    fun setMediaStreamCategoryC(participantId: String, quality: MediaStreamQuality)
```

Define the video quality options:

```swift
 enum MediaStreamQuality {
     case Undefined
     case LD  // 180p
     case SD  // 360p
     case HD  // 720p
     case FHD // 1080p
 }
```

### 2. Remove a Pinned Stream

To unpin a participant's stream:

```swift
fun removeMediaStreamCategoryC(participantId: String)
```

### 3. Check for Pinning Support

To determine if stream pinning is supported:

```swift
var isMediaStreamsPinningSupported : Boolean
```

### 4. Listen for Media Stream Changes

To listen for changes in media stream properties, register a change listener to handle events:

```swift
 enum MediaStreamChangeEventType {
    case Size
    case Membership
    case Video
    case Audio
    case PinState
}
```

```swift
stream.setOnMediaStreamInfoChanged { type, info in
    // type: MediaStreamChangeEventType
    // info: MediaStreamChangeEventInfo
}
```
