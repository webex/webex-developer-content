---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/ios-meetings-sdk-multistream
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Pin Participant Streams
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
