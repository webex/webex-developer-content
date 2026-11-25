---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/android-calling-sdk-quickstart
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Check Feature Entitlements for a Logged-In User
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/android-calling-sdk-quickstart). [Full Markdown](../../../../../docs/sdks/android-calling-sdk-quickstart.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This guide provides the fundamental steps for integrating calling features into your Android application using the Webex Android Mobile SDK. For comprehensive parameters and methods, please refer to the [SDK API Reference](https://developer.webex.com/docs/sdks/android-sdk-overview#sdk-api-reference).

---

At the core of the SDK is the `Webex` object, serving as the gateway to all SDK functionalities. The `Call` object represents an active call and provides methods to manage various aspects of the call lifecycle, such as answering, hanging up, muting, and unmuting. You obtain a `Call` object either as a result of a successful outgoing call through the `dial` method or as an incoming call event.



> **Info**
>
> Methods are largely consistent between Unified Communications Manager (UCM) and Webex Calling.

## Selected section

## Check Feature Entitlements for a Logged-In User

The user's license determines their access to meeting, messaging, and calling features. Use `webex.people.getProductCapability()` to verify the user's entitlements.

```kotlin
var capability = webex.people.getProductCapability()

var hasCalling = capability.isCallingSupported()
var hasMessaging = capability.isMessagingSupported()
var hasMeeting = capability.isMeetingSupported()
```
