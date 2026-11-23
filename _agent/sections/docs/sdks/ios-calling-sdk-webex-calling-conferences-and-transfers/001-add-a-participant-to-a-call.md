---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/ios-calling-sdk-webex-calling-conferences-and-transfers
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Add a Participant to a Call
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/ios-calling-sdk-webex-calling-conferences-and-transfers). [Full Markdown](../../../../../docs/sdks/ios-calling-sdk-webex-calling-conferences-and-transfers.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article offers a deep dive into the sophisticated features that allow for the expansion and redirection of calls within a network.

It explores the mechanisms behind adding participants to an ongoing call, facilitating assisted transfers with the involvement of a third party, and executing direct transfers for immediate call redirection. Whether it's merging multiple calls into a conference or deftly transferring a call to another participant, these features ensure that conversations can evolve and adapt without missing a beat.

## Selected section

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
