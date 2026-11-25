---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/android-messaging-sdk-quickstart
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Check Feature Entitlements for a Logged-In User
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/android-messaging-sdk-quickstart). [Full Markdown](../../../../../docs/sdks/android-messaging-sdk-quickstart.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article provides examples of common methods used in the meetings flow for the iOS Messaging SDK. For detailed method parameters, refer to the [SDK API Reference](https://developer.webex.com/docs/sdks/android-sdk-overview#sdk-api-reference).

---

The `Webex` instance is the primary entry point for the SDK, allowing access to all Webex SDK APIs.

## Selected section

## Check Feature Entitlements for a Logged-In User

To determine what entitlements a particular logged-in user has:

```kotlin
var capability = webex.people.getProductCapability()

var hasCalling = capability.isCallingSupported()
var hasMessaging = capability.isMessagingSupported()
var hasMeeting = capability.isMeetingSupported()
```
