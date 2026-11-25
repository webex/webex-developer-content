---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/android-calling-sdk-ucm-basic-usage
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Use UCM Phone Services
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/android-calling-sdk-ucm-basic-usage). [Full Markdown](../../../../../docs/sdks/android-calling-sdk-ucm-basic-usage.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Follow the steps in this article to begin using Cisco Unified Communications Manager (CUCM, or UCM for short) in your Android application.

---

# Android Calling SDK | UCM Basic Usage

Follow the steps in this article to begin using Cisco Unified Communications Manager (CUCM, or UCM for short) in your Android application.

## Selected section

## Use UCM Phone Services

1. Make a call:

    Use `dialPhoneNumber` for PSTN or `dial` for other types.

    ```kotlin
    val mediaOption = MediaOption.audioOnly()
    webex.phone.dialPhoneNumber("+1800123456", mediaOption, CompletionHandler { result ->
        if (result.isSuccessful) {
            // Call started successfully, result.data gives you a Call object
        } else {
            // Call failed, result.error gives you the error code. The error code will be an instance of WebexError.ErrorCode
        }
    })
    ```

    

> **Info**
>
> The `dialPhoneNumber` API is available starting with version 3.9.2.



1. Transfer a call:

    ```kotlin
    // Hold the current ongoing call before associating to another call
    call?.holdCall(true, CompletionHandler { result ->
        if (result.isSuccessful) {
            // Call hold successful
        } else {
            // Call hold failed
        }
    })
    ```

    ```kotlin
    // Proceed if hold succeeds
    call?.startAssociatedCall("+1800123457", associationType = CallAssociationType.Transfer, audioCall = true, CompletionHandler { result ->
            if (result.isSuccessful) {
                // Call association is successful; result.data returns a new Call object.
                val newCall: Call? = result.data
                // Transfer the call.
                call?.transferCall(newCall?.getCallId())
            } else {
                // Call association failed.
            }
        })
    ```  

1. Merge a call:

    ```kotlin
    // Put the active call on hold.
    call?.holdCall(true, CompletionHandler { result ->
        if (result.isSuccessful) {
            // Call hold successful
        } else {
            // Call hold failed
        }
    })
    ```

    ```kotlin
    // If hold succeeds, start a new call that can be merged later with the existing call.
    call?.startAssociatedCall("+1800123457", associationType = CallAssociationType.Merge, audioCall = true, CompletionHandler { result ->
        if (result.isSuccessful) {
            // Call association is successful; result.data returns a new Call object.
            val newCall: Call? = result.data
            // Merge the calls.
            call?.mergeCalls(newCall?.getCallId())
        } else {
            // Call association failed.
        }
    })
    ```

1. Logout of UCM:

    ```kotlin
    webex.authenticator?.deauthorize(CompletionHandler { result ->
        if (result.isSuccessful) {
            // Logged out of UCM and Webex services successfully
        } else {
            // Logout failed; result.error?.errorMessage provides more details.
        }
    })
    ```

    

> **Info**
>
> If the SSO login is in progress and the user cancels the login flow, the SSO flow should be canceled by calling the `webex.ucCancelSSOLogin()` method.
