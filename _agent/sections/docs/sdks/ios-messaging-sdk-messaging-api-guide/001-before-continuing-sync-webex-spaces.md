---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/ios-messaging-sdk-messaging-api-guide
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- 'Before Continuing: Sync Webex Spaces'
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/ios-messaging-sdk-messaging-api-guide). [Full Markdown](../../../../../docs/sdks/ios-messaging-sdk-messaging-api-guide.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article provides detailed information on the messaging features and methods provided by the Webex iOS Messaging SDK.

---

The SDK lets you easily implement real-time messaging capabilities including posting new messages, and deleting, listing, and editing existing messages.

## Selected section

## Before Continuing: Sync Webex Spaces

Before working with spaces or messages within them, ensure that all spaces are synced using the following method:

```swift
// Indicates if the latest conversations have been synced to the local data warehouse.
// Returns true if the sync is completed.
// Returns false if the sync is in progress.
webex.spaces.isSpacesSyncCompleted 
    
// The callback handler for sync status changes.
webex.spaces.onSyncingSpacesStatusChanged = { isSpacesSyncInProgress in
    // isSpacesSyncInProgress is true if a space sync is in progress.
    // isSpacesSyncInProgress is false if a space sync is complete.
 }
```

![Messaging Flow Diagram](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltadc14f928a4816b3/222117387-a9888f35-be35-4af9-aac7-5c5acf601aef.png)
