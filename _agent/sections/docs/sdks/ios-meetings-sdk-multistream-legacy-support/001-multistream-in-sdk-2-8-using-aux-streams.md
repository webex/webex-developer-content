---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/ios-meetings-sdk-multistream-legacy-support
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Multistream in SDK 2.8 Using Aux Streams
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/ios-meetings-sdk-multistream-legacy-support). [Full Markdown](../../../../../docs/sdks/ios-meetings-sdk-multistream-legacy-support.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article provides details on how to use multistream features in older versions of the Webex Mobile SDK.

---

It serves as a reference for legacy implementations, but it is highly recommended to use the latest Webex Mobile SDKs and refer to the newer [Multistream](https://developer.webex.com/docs/sdks/ios-meetings-sdk-multistream) documentation for the current implementations.

![Multistream Example](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt8efd63a7f9794b20/multistream.jpeg)

## Selected section

## Multistream in SDK 2.8 Using Aux Streams

Multistream allows participants to see the video of the most active speakers in a meeting. Each video stream is known as an auxiliary stream. Auxiliary streams can display active participants, with the primary active speaker shown on the main remote video view and other active speakers on auxiliary video views.

![Image described in the surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt5e2690071b433887/IMG_0910.jpg)

### Typical Scenario in SDK 2.8

In meetings with more than two participants, use multistream to view the active speaker and other participants.

### Limitations in SDK 2.8

Please be aware of the following limitations:

- A maximum of 4 auxiliary video streams are allowed.
- The stream for a specific participant is based on activity, not selection.
