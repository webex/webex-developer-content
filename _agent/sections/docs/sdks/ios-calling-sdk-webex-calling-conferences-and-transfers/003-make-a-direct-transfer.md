---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/ios-calling-sdk-webex-calling-conferences-and-transfers
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Make a Direct Transfer
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/ios-calling-sdk-webex-calling-conferences-and-transfers). [Full Markdown](../../../../../docs/sdks/ios-calling-sdk-webex-calling-conferences-and-transfers.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article offers a deep dive into the sophisticated features that allow for the expansion and redirection of calls within a network.

It explores the mechanisms behind adding participants to an ongoing call, facilitating assisted transfers with the involvement of a third party, and executing direct transfers for immediate call redirection. Whether it's merging multiple calls into a conference or deftly transferring a call to another participant, these features ensure that conversations can evolve and adapt without missing a beat.

## Selected section

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
