---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/android-meetings-sdk-quickstart
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Display Remote Screen Share
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/android-meetings-sdk-quickstart). [Full Markdown](../../../../../docs/sdks/android-meetings-sdk-quickstart.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article provides examples of common API usage within the meetings flow. For detailed API information, please refer to the [SDK API Reference](https://developer.webex.com/docs/sdks/android-sdk-overview#sdk-api-reference).

---

The `Webex` instance serves as the primary entry point for the SDK, providing access to all Webex SDK APIs. The `Call` object represents a meeting and offers APIs for actions such as joining, leaving, muting, and unmuting. The `Call` object is returned as a result of a successful `dial` API call.

## Selected section

## Display Remote Screen Share

To display the screen share from the remote party:

```kotlin
webex.phone.dial("spaceId", MediaOption.audioVideoSharing(Pair(localView, remoteView), screenShareView), CompletionHandler {
    if(it.isSuccessful){
        val call = it.data
        call?.setObserver(object :CallObserver{
            override fun onConnected(call: Call?) {
                super.onConnected(call)
            }

            // ...

            override fun onMediaChanged(event: CallObserver.MediaChangedEvent?) {
                event?.let { _event ->
                    val _call = _event.getCall()
                    when (_event) {
                        is CallObserver.RemoteSendingSharingEvent -> {
                            if (_event.isSending()) {
                                _call?.setSharingRenderView(screenShareView)
                            } else {
                                _call??.setSharingRenderView(null)
                            }
                        }
                    }
                }
            }
        })
    } else {
        val error = it.error
    }
})
```
