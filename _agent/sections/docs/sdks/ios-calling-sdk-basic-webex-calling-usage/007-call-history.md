---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/ios-calling-sdk-basic-webex-calling-usage
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Call history
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/ios-calling-sdk-basic-webex-calling-usage). [Full Markdown](../../../../../docs/sdks/ios-calling-sdk-basic-webex-calling-usage.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article outlines the fundamental steps for integrating call functionality using the Webex iOS SDK.

## Selected section

## Call history

The SDK provides call history functionality to retrieve, manage, and monitor call records from One-to-One direct calls.
    
1. Get call history records
    ```swift
    // Returns a collection of CallHistoryRecord objects containing
    let callHistoryItems = webex.phone.getCallHistory()
    ```

2. Remove call history records
   ```swift
   // Removes specific call history records using their unique identifiers
   // Use the record IDs obtained from getCallHistory() or event callbacks
   webex.phone.removeCallHistoryRecords(recordIds: [recordIdToDelete])
   ```

3. Register for call history events
   ```swift
   webex.phone.onCallHistoryEvent = { [weak self] (event) in
       switch event {
       case .syncCompleted:
           // Call history synchronization completed
       case .removed(let recordIds):
           // Call history records removed successfully
       case .removeFailed:
           // Call history record removal failed
       }
   }
   ```
