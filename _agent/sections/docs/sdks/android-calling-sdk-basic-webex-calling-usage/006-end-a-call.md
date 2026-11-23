---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/android-calling-sdk-basic-webex-calling-usage
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- End a call
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/android-calling-sdk-basic-webex-calling-usage). [Full Markdown](../../../../../docs/sdks/android-calling-sdk-basic-webex-calling-usage.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article outlines the fundamental steps for integrating call functionality using the Webex Android SDK.

## Selected section

## End a call

End a connected call using the `call.hangup()` method:

```kotlin
call?.hangup(CompletionHandler { result ->
        if (result.isSuccessful) {
            // Call has ended. Handle cleanup.
        } else {
            // Ending the call failed.
        }
    })
```
