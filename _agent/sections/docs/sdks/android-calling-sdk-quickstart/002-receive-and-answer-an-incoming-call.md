---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/android-calling-sdk-quickstart
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Receive and Answer an Incoming Call
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/android-calling-sdk-quickstart). [Full Markdown](../../../../../docs/sdks/android-calling-sdk-quickstart.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This guide provides the fundamental steps for integrating calling features into your Android application using the Webex Android Mobile SDK. For comprehensive parameters and methods, please refer to the [SDK API Reference](https://developer.webex.com/docs/sdks/android-sdk-overview#sdk-api-reference).

---

At the core of the SDK is the `Webex` object, serving as the gateway to all SDK functionalities. The `Call` object represents an active call and provides methods to manage various aspects of the call lifecycle, such as answering, hanging up, muting, and unmuting. You obtain a `Call` object either as a result of a successful outgoing call through the `dial` method or as an incoming call event.



> **Info**
>
> Methods are largely consistent between Unified Communications Manager (UCM) and Webex Calling.

## Selected section

## Receive and Answer an Incoming Call

Set a incoming call listener using the `setIncomingCallListener()` method. If the `Call` object intercepted by the `onIncomingCall()` method is not null, answer it using the `Call` objects's answer method:

```kotlin
webex.phone.setIncomingCallListener(object : Phone.IncomingCallListener {
    override fun onIncomingCall(call: Call?) {
        call?.answer(MediaOption.audioOnly(), CompletionHandler { // use MediaOption.audioVideo() for video webex call. 
            if (it.isSuccessful){
                // The call is answered.
            }
        })
    }
})
```
