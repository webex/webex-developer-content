---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/android-calling-sdk-webex-calling-conferences-and-transfers
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Add a Participant to a Call
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/android-calling-sdk-webex-calling-conferences-and-transfers). [Full Markdown](../../../../../docs/sdks/android-calling-sdk-webex-calling-conferences-and-transfers.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article offers a deep dive into the sophisticated features that allow for the expansion and redirection of calls within a network.

It explores the mechanisms behind adding participants to an ongoing call, facilitating assisted transfers with the involvement of a third party, and executing direct transfers for immediate call redirection. Whether it's merging multiple calls into a conference or deftly transferring a call to another participant, these features ensure that conversations can evolve and adapt without missing a beat.

## Selected section

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
