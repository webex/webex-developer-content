---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/android-calling-sdk-webex-calling-conferences-and-transfers
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Make a Direct Transfer
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/android-calling-sdk-webex-calling-conferences-and-transfers). [Full Markdown](../../../../../docs/sdks/android-calling-sdk-webex-calling-conferences-and-transfers.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article offers a deep dive into the sophisticated features that allow for the expansion and redirection of calls within a network.

It explores the mechanisms behind adding participants to an ongoing call, facilitating assisted transfers with the involvement of a third party, and executing direct transfers for immediate call redirection. Whether it's merging multiple calls into a conference or deftly transferring a call to another participant, these features ensure that conversations can evolve and adapt without missing a beat.

## Selected section

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
