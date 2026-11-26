---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/android-calling-sdk-basic-webex-calling-usage
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Hold or Resume a Call
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/android-calling-sdk-basic-webex-calling-usage). [Full Markdown](../../../../../docs/sdks/android-calling-sdk-basic-webex-calling-usage.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article outlines the fundamental steps for integrating call functionality using the Webex Android SDK.

## Selected section

## Hold or Resume a Call

To hold a call:

```kotlin
call?.holdCall(true, CompletionHandler { result ->
    if (result.isSuccessful) {
        // Call hold successful
    } else {
        // Call hold failed
    }
})
```

To resume a call:

```kotlin
call?.holdCall(false, CompletionHandler { result ->
    if (result.isSuccessful) {
        // Call hold successful
    } else {
        // Call hold failed
    }
})
```

Check if a call is on hold:

```kotlin
var isOnHold = call?.isOnHold() : false
```
