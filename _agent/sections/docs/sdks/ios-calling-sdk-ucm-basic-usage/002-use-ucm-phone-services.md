---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/ios-calling-sdk-ucm-basic-usage
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Use UCM Phone Services
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/ios-calling-sdk-ucm-basic-usage). [Full Markdown](../../../../../docs/sdks/ios-calling-sdk-ucm-basic-usage.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Follow the steps in this guide to begin using Cisco Unified Communications Manager (CUCM, or UCM for short) in your iOS application.

## Selected section

## Use UCM Phone Services

To use UCM phone services once you've verified your connection:

1. Make a call.

    Use `dialPhoneNumber` for PSTN or `dial` for other call types:

    ```swift
    let mediaOption = MediaOption.audioOnly()
     webex.phone.dialPhoneNumber("+1800123456", option: mediaOption) { result in
        switch result {
           case .success(let call):
                 // Call started successfully.
            case .failure(let error):
                // Call failed.
        }
    }
    ```

    

> **Info**
>
> The `dialPhoneNumber` API is available starting with version 3.9.2.



1. Transfer a call:

    ```swift
    guard call.isCUCMCall else { 
        print("Call transfer works only with UCM calls")
        return
    }

    // Put an active call on hold
    call.holdCall(putOnHold: true) { error in 
        if(error != nil) {
            // hold success
        }
    }
    
    // Start a new call that can be transferred later to the previous call
    call.startAssociatedCall( dialNumber: "+1800123123", associationType: .transfer, isAudioCall: true) {[weak self] result in
        switch result {
        case .success(let newCall):
            // Successfully started an associated call that can be transferred
            call.transferCall(toCallId: newCall.callId)
        case .failure(let error):
            // An error occurred
        }
    }  
    ```

1. Merge a call:

    ```swift
    guard call.isCUCMCall else { 
        print("Call merge works only with CUCM calls.")
        return
    }

    // Put an active call on hold:
    call.holdCall(putOnHold: true) { error in 
        if(error != nil) {
            // hold success
        }
    }
    
    // Start a new call that can be merged later with the existing call.
    call.startAssociatedCall(dialNumber: "+1800123123", associationType: .merge, isAudioCall: true) {[weak self] result in
        switch result {
        case .success(let newCall):
            // Merge the calls.
            call.mergeCall(targetCallId: newCall.callId)
        case .failure(let error):
            // An error occurred.
        }
    }  
    ```
