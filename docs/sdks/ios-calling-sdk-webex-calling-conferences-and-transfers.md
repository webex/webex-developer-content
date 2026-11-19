---
type: Guide
title: iOS Calling SDK | Webex Calling Conferences and Transfers
display_title: Conferences and Transfers
canonical_url: https://developer.webex.com/docs/sdks/ios-calling-sdk-webex-calling-conferences-and-transfers
content_type: documentation
product_group:
- webex-suite
categories:
- calling
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/ios-calling-sdk-webex-calling-conferences-and-transfers)

This article offers a deep dive into the sophisticated features that allow for the expansion and redirection of calls within a network.

It explores the mechanisms behind adding participants to an ongoing call, facilitating assisted transfers with the involvement of a third party, and executing direct transfers for immediate call redirection. Whether it's merging multiple calls into a conference or deftly transferring a call to another participant, these features ensure that conversations can evolve and adapt without missing a beat.

## Add a Participant to a Call

To add a participant to a call:

1. Hold the current active call:

    ```swift
    oldCall?.holdCall(putOnHold: true) { error in 
        if(error != nil) {
            // hold success
        }
    }
    ```

2. Initiate a call with the new participant:

    

> **Info**
>
> Prompt the user with a dial pad to capture the new participant's number and initiate a new call that can be merged later.



    ```swift
    call.startAssociatedCall(dialNumber: "+1800123457", associationType: .Merge, isAudioCall: true, completionHandler: { [weak self] result in
        switch result {
        case .success(let call):
            // Call association is successful.
            let newCall: Call? = call
            // Store this call object.
        case .failure(let error):
            // Call association failed.
        }
    })
    ````

3. Merge the old call with the new one:

    ```swift
    newCall.mergeCall(targetCallId: oldCall.callId)
    ```



> **Info**
>
> It is possible to add a participant to one call while keeping another call on hold, even when two calls are active.



## Make an Assisted Transfer

In an assisted transfer, the initiator (User A) connects with a third party (User C) and transfers the call so that the original party (User B) and the third party (User C) remain connected, while the initiator drops out after establishing the connection.

1. Hold the current active call:

    ```swift
    oldCall?.holdCall(putOnHold: true) { error in 
        if(error != nil) {
            // hold success
        }
    }
    ```

2. Start a call with the new participant for the transfer:

    

> **Info**
>
> Prompt the user with a dial pad to capture the new participant's number and initiate a new call that can be transferred.



    ```swift
    call.startAssociatedCall(dialNumber: "+1800123457", associationType: .Transfer, isAudioCall: true, completionHandler: { [weak self] result in
        switch result {
        case .success(let call):
            // Call association is successful.
            let newCall: Call? = call
            // Store this call object.
        case .failure(let error):
            // Call association failed.
        }
    })
    ```

3. Transfer the call to the new participant:

    ```swift
    oldCall.transferCall(toCallId: newCall.callId)
    ```



> **Info**
>
> Assisted transfers can be performed with two active calls, allowing a user to transfer one call while resuming another call in the queue.



## Make a Direct Transfer

To transfer a call directly to another participant without establishing a call:

```swift
call?.directTransferCall(toPhoneNumber: phoneNumber, completionHandler: { err in
    if err == nil {
        // Direct transfer is successful.
    }
    else
    {
        // Direct transfer failed.
    }
})
 ```



> **Info**
>
> Direct transfers are immediate and do not require the new call to be answered before completing the transfer.
