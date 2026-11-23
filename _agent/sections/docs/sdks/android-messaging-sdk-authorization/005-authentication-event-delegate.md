---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/android-messaging-sdk-authorization
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Authentication Event Delegate
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/android-messaging-sdk-authorization). [Full Markdown](../../../../../docs/sdks/android-messaging-sdk-authorization.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

The Webex Mobile Android SDK must be initialized and authorized to interact with the Webex platform. Your application should authenticate users through an [OAuth](https://oauth.net/) grant flow for existing Cisco Webex users or a JSON web token (JWT) for guest users without a Cisco Webex account.

---

This article provides code examples explaining how to perform this authorization using either a built in Webview or an external browser.

## Selected section

## Authentication Event Delegate

Extend the `WebexAuthDelegate` interface to receive authentication-related event callbacks.

```kotlin
interface WebexAuthDelegate {
    /**
     * This notifies when user is logged out and re-login is required.
     */
    fun onReLoginRequired() {}
}
```

Example usage:

```kotlin
class SomeClass : WebexAuthDelegate {
    ...
    override fun onReLoginRequired() {
        // Handle signout and perform any cleanup if required.
    }
    ...
}
```
