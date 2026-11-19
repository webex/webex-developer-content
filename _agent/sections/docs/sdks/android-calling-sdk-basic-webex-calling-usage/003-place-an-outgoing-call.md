---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/android-calling-sdk-basic-webex-calling-usage
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Place an Outgoing Call
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/android-calling-sdk-basic-webex-calling-usage). [Full Markdown](../../../../../docs/sdks/android-calling-sdk-basic-webex-calling-usage.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article outlines the fundamental steps for integrating call functionality using the Webex Android SDK.

## Selected section

## Place an Outgoing Call

When phone services are active, you can make outgoing calls to any Webex calling or PSTN number using `webex.phone.dialPhoneNumber()`. Note that attempting to dial anything other than phone numbers with `webex.phone.dialPhoneNumber()` will result in a call failure, indicated by `INVALID_API_ERROR`.

```kotlin
val mediaOption = MediaOption.audioOnly()
webex.phone.dialPhoneNumber("+1800123456", mediaOption, CompletionHandler { result ->
    if (result.isSuccessful) {
        // Dial out is successful; result.data returns a Call object.
        // Store the Call object for further use.
        val call = result.data
        call?.setObserver(object : CallObserver {
            override fun onConnected(call: Call?) {
                super.onConnected(call)
            }

            override fun onDisconnected(event: CallObserver.CallDisconnectedEvent?) {
                super.onDisconnected(event)
            }

            override fun onRinging(call: Call?) {
                super.onRinging(call)
            }
        })
    } else {
        // Dialing failed; result.error, an instance of WebexError.ErrorCode, provides more details.
    }
})
```



> **Info**
>
> The `dialPhoneNumber()` method is available from v3.9.2 and later.
