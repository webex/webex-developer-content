---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/android-meetings-sdk-multistream-legacy-support
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Multistream in SDK 2.8 Using Aux Streams
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/android-meetings-sdk-multistream-legacy-support). [Full Markdown](../../../../../docs/sdks/android-meetings-sdk-multistream-legacy-support.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article provides details on how to use multistream features in older versions of the Webex Mobile SDK.

---

However, we highly recommend using the latest Webex Mobile SDKs. Refer to the newer [Multistream](https://developer.webex.com/docs/sdks/android-meetings-sdk-multistream) documentation for the current implementation.

## Selected section

## Multistream in SDK 2.8 Using Aux Streams

Multistream allows participants to see the video of the most active speakers in a meeting. Each video stream is known as an auxiliary stream. Auxiliary streams can display active participants, with the primary active speaker shown on the main remote video view and other active speakers on auxiliary video views.

![Multistream-example](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt76accc9a83783b10/Screenshot_20180907-164030.png)

### Typical Scenario in SDK 2.8

In meetings with more than two participants, use multistream to view the active speaker and other participants.

### Limitations in SDK 2.8

Please be aware of the following limitations:

- A maximum of 4 auxiliary video streams are allowed.
- The stream for a specific participant is based on activity, not selection.
