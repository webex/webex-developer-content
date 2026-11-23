---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/android-meetings-sdk-multistream-legacy-support
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Multistream in SDK 3.0 Using Aux Streams
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/android-meetings-sdk-multistream-legacy-support). [Full Markdown](../../../../../docs/sdks/android-meetings-sdk-multistream-legacy-support.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article provides details on how to use multistream features in older versions of the Webex Mobile SDK.

---

However, we highly recommend using the latest Webex Mobile SDKs. Refer to the newer [Multistream](https://developer.webex.com/docs/sdks/android-meetings-sdk-multistream) documentation for the current implementation.

## Selected section

## Multistream in SDK 3.0 Using Aux Streams

Multistream displays the video of the most active participants. Streams are allocated based on the order of joining, and participants exceeding the limit are placed in a queue. Active speakers can take over streams, and when participants leave, others from the queue will replace them.

![Multistream example](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt4e03685952149e13/multistream.png)

### Limitations in SDK 3.0

Please be aware of the following limitations:

- A maximum of 4 auxiliary video streams are allowed.
- The stream for a specific participant is based on activity, not selection.
