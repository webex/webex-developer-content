---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/ios-messaging-sdk-monitor-presence
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Stop Watching Presence
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/ios-messaging-sdk-monitor-presence). [Full Markdown](../../../../../docs/sdks/ios-messaging-sdk-monitor-presence.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Presence Status provides real-time status updates about contacts which include predefined states, custom messages and state-specific expiration and last active times.

---

The presence related methods can be accessed through the `PersonClient` object.



> **Info**
>
> Available starting from SDK version 3.10.0.

## Selected section

## Stop Watching Presence

To stop presence updates use the `webex.people.stopWatchingPresences()` method, passing in presence handles:

```swift
webex.people.stopWatchingPresences(presenceHandles: presenceHandles)
```
