---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/ios-meetings-sdk-multistream-legacy-support
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Multistream in SDK 3.0 Using Aux Streams
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/ios-meetings-sdk-multistream-legacy-support). [Full Markdown](../../../../../docs/sdks/ios-meetings-sdk-multistream-legacy-support.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article provides details on how to use multistream features in older versions of the Webex Mobile SDK.

---

It serves as a reference for legacy implementations, but it is highly recommended to use the latest Webex Mobile SDKs and refer to the newer [Multistream](https://developer.webex.com/docs/sdks/ios-meetings-sdk-multistream) documentation for the current implementations.

![Multistream Example](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt8efd63a7f9794b20/multistream.jpeg)

## Selected section

## Multistream in SDK 3.0 Using Aux Streams

Multistream lets you view multiple active participants in a meeting:

- Stream order is based on the order of joining.
- Beyond 6 participants (self, remote, and auxiliary streams), extra participants queue up and aren't allocated streams.
- Active participants from the queue replace less active streams.
- Departing participants' streams are replaced by queued participants.
- Use the [Active Speaker Method](https://webex.github.io/webex-ios-sdk/Structs/CallMembership.html#/s:8WebexSDK14CallMembershipV15isActiveSpeakerSbvp) to identify the active speaker.
- The [ActiveSpeakerChangedEvent](https://webex.github.io/webex-ios-sdk/Classes/Call/MediaChangedEvent.html#/s:8WebexSDK4CallC17MediaChangedEventO013activeSpeakereF0yAeA0C10MembershipVSg_AItcAEmF) triggers when the active speaker changes.

### Typical Scenario in SDK 3.0

Use multistream in meetings with more than two participants to view the active speaker and others.

### Limitations in SDK 3.0

- You can display a maximum of 4 streams.
- Specific participant streams cannot be chosen; activity determines allocation.
