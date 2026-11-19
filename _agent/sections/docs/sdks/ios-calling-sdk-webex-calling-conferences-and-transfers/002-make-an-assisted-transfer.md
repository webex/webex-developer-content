---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/ios-calling-sdk-webex-calling-conferences-and-transfers
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Make an Assisted Transfer
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/ios-calling-sdk-webex-calling-conferences-and-transfers). [Full Markdown](../../../../../docs/sdks/ios-calling-sdk-webex-calling-conferences-and-transfers.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article offers a deep dive into the sophisticated features that allow for the expansion and redirection of calls within a network.

It explores the mechanisms behind adding participants to an ongoing call, facilitating assisted transfers with the involvement of a third party, and executing direct transfers for immediate call redirection. Whether it's merging multiple calls into a conference or deftly transferring a call to another participant, these features ensure that conversations can evolve and adapt without missing a beat.

## Selected section

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
