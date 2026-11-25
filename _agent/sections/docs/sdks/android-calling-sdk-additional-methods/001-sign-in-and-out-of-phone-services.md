---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/android-calling-sdk-additional-methods
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Sign in and Out of Phone Services
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/android-calling-sdk-additional-methods). [Full Markdown](../../../../../docs/sdks/android-calling-sdk-additional-methods.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article describes additional methods available in the Webex Calling Android SDK.

---



> **Info**
>
> The Mobile SDK supports a maximum of two concurrent incoming calls. A third incoming call is automatically ignored or silently dismissed. Only one call can be in a resumed state at any time.

## Selected section

## Sign in and Out of Phone Services

Applications can disconnect from Webex calling phone services, enabling users to cease making and receiving calls while continuing to use other features, such as messaging and meetings.

### Sign in to Phone Services

To sign in to phone services:

```kotlin
webex.phone.connectPhoneServices{ result ->
    if (result.isSuccessful) {
        // Connecting to phone services succeeded
    } else {
        // Connecting to phone services failed
    }
}
```



> **Info**
>
> The actual phone service status is available in the `onUCServerConnectionStateChanged` callback.



### Sign out of phone services

To sign out of phone services:

```kotlin
webex.phone.disconnectPhoneServices{ result ->
    if (result.isSuccessful) {
        // Disconnecting from phone services succeeded
    } else {
        // Disconnecting from phone services failed
    }
}
```



> **Info**
>
> The actual phone service status is available in the `onUCServerConnectionStateChanged` callback.
