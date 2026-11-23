---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/android-meetings-sdk-quickstart
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Join a Meeting
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/android-meetings-sdk-quickstart). [Full Markdown](../../../../../docs/sdks/android-meetings-sdk-quickstart.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article provides examples of common API usage within the meetings flow. For detailed API information, please refer to the [SDK API Reference](https://developer.webex.com/docs/sdks/android-sdk-overview#sdk-api-reference).

---

The `Webex` instance serves as the primary entry point for the SDK, providing access to all Webex SDK APIs. The `Call` object represents a meeting and offers APIs for actions such as joining, leaving, muting, and unmuting. The `Call` object is returned as a result of a successful `dial` API call.

## Selected section

## Join a Meeting

To join a meeting with the `dial` API by providing a meeting ID, SIP address, or meeting link:

```kotlin
webex.phone().dial(meetingId, MediaOption.audioVideoSharing(Pair(localView,remoteView), screenShareView), CompletionHandler { result ->
    if (result.isSuccessful) {
        result.data?.let { _call ->
            // Space call connected. Set observer to listen for call events
            call.setObserver(object : CallObserver {
                override fun onConnected(call: Call?) {
                }

                override fun onRinging(call: Call?) {
                }

                override fun onWaiting(call: Call?, reason: Call.WaitReason?) {
                }

                override fun onDisconnected(event: CallObserver.CallDisconnectedEvent?) {
                }

                override fun onInfoChanged(call: Call?) {
                }

                override fun onMediaChanged(event: CallObserver.MediaChangedEvent?) {
                }

                override fun onCallMembershipChanged(event: CallObserver.CallMembershipChangedEvent?) {
                }

                override fun onScheduleChanged(call: Call?) {
                }
            })
        }
    } else {
        result.error?.let { errorCode ->
            // Error in space call
        }
    }
});
```
