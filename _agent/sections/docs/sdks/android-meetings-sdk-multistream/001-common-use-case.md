---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/android-meetings-sdk-multistream
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Common Use Case
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

## Common Use Case

For meetings with more than two participants, multistream can display the active speaker and other attendees simultaneously.
