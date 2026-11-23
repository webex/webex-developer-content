---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/ios-calling-sdk-basic-webex-calling-usage
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Query Phone Services Status
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/ios-calling-sdk-basic-webex-calling-usage). [Full Markdown](../../../../../docs/sdks/ios-calling-sdk-basic-webex-calling-usage.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article outlines the fundamental steps for integrating call functionality using the Webex iOS SDK.

## Selected section

## Query Phone Services Status

To check the current status of phone services, use the `webex.getUCServerConnectionStatus()` method:

```swift
let phoneServicesStatus = webex.getUCServerConnectionStatus()
if (phoneServicesStatus == UCLoginServerConnectionStatus.Connected) {
    // Indicates that phone services are ready.
}
```
