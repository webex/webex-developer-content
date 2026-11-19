---
type: Guide
title: Android Calling SDK | Webex Calling Conferences and Transfers
display_title: Conferences and Transfers
canonical_url: https://developer.webex.com/docs/sdks/android-calling-sdk-webex-calling-conferences-and-transfers
content_type: documentation
product_group:
- webex-suite
categories:
- calling
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/android-calling-sdk-webex-calling-conferences-and-transfers)

This article offers a deep dive into the sophisticated features that allow for the expansion and redirection of calls within a network.

It explores the mechanisms behind adding participants to an ongoing call, facilitating assisted transfers with the involvement of a third party, and executing direct transfers for immediate call redirection. Whether it's merging multiple calls into a conference or deftly transferring a call to another participant, these features ensure that conversations can evolve and adapt without missing a beat.

## Add a Participant to a Call

To add an additional participant to an ongoing call, follow these steps:

1. Hold the current active call:

    ```kotlin
    oldCall?.holdCall(true, CompletionHandler { result ->
        if (result.isSuccessful) {
            // Call hold successful
        } else {
            // Call hold failed
        }
    })
    ```

2. Initiate a call with the new participant:

    

> **Info**
>
> Prompt the user with a dial pad to capture the new participant's number and initiate a new call that can be merged later.



    ```kotlin
    call?.startAssociatedCall("+1800123457", associationType = CallAssociationType.Merge, audioCall = true, CompletionHandler { result ->
            if (result.isSuccessful) {
                // Call association is successful; result.data returns a new Call object.
                val newCall: Call? = result.data
                // Store the Call object.
            } else {
                // Call association failed.
            }
        })
    ```

3. Merge the old call with the new one:

    ```kotlin
    newCall?.mergeCalls(oldCall.getCallId())
    ```



> **Info**
>
> It is possible to add a participant to one call while keeping another call on hold, even when two calls are active.



## Assisted transfers

In an assisted transfer, the initiator (User A) connects with a third party (User C) and transfers the call so that the original party (User B) and the third party (User C) remain connected, while the initiator drops out after establishing the connection.

1. Hold the current active call:

    ```kotlin
    oldCall?.holdCall(true, CompletionHandler { result ->
        if (result.isSuccessful) {
            // Call hold successful
        } else {
            // Call hold failed
        }
    })
    ```

2. Start a call with the new participant for the transfer:

    

> **Info**
>
> Prompt the user with a dial pad to capture the new participant's number and initiate a new call that can be transferred.



    ```kotlin
    call?.startAssociatedCall("+1800123457", associationType = CallAssociationType.Transfer, audioCall = true, CompletionHandler { result ->
        if (result.isSuccessful) {
            // Call association is successful, result.data gives new Call object
            val newCall: Call? = result.data
            // Store this call object
        } else {
            // Call association failed
        }
    }) 
    ```

3. Transfer the call to the new participant:

    ```kotlin
    oldCall?.transferCall(newCall.getCallId())
    ```



> **Info**
>
> Assisted transfers can be performed with two active calls, allowing a user to transfer one call while resuming another call in the queue.



## Make a Direct Transfer

For a direct transfer, where the call is transferred to another participant without prior consultation, the application captures the new participant's number and uses the direct transfer method:

```kotlin
call?.directTransferCall(toPhoneNumber, CompletionHandler { result ->
    if (result.isSuccessful) {
        // Direct transfer successful.
    } else {
        // Direct transfer failed.
    }
})
```



> **Info**
>
> Direct transfers are immediate and do not require the new call to be answered before completing the transfer.
