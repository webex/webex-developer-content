---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/ios-meetings-sdk-quickstart
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Verify Feature Entitlements
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/ios-meetings-sdk-quickstart). [Full Markdown](../../../../../docs/sdks/ios-meetings-sdk-quickstart.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This guide provides examples of common methods used in the meetings flow for the iOS Meetings SDK. For detailed method parameters, refer to the [SDK API Reference](https://developer.webex.com/docs/sdks/ios-sdk-overview#sdk-api-reference).

---

The `Webex` instance is the core access point for the SDK, providing access to all Webex SDK methods. A `Call` object represents a meeting and includes methods for joining, leaving, muting, unmuting, and other actions. This object is returned as a result of a successful `dial` method invocation.

## Selected section

## Verify Feature Entitlements

Features such as messaging, meeting, and calling depend on the logged-in user's license. The `webex.people.getProductCapability()` method verifies a user's entitlements:

```swift
let capability: ProductCapability = webex.people.getProductCapability()
let hasCalling = capability.isCallingSupported
let hasMeeting = capability.isMeetingSupported
let hasMessaging = capability.isMessagingSupported
```
