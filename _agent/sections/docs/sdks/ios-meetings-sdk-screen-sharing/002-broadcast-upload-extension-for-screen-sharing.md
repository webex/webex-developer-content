---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/ios-meetings-sdk-screen-sharing
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Broadcast Upload Extension for Screen Sharing
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/ios-meetings-sdk-screen-sharing). [Full Markdown](../../../../../docs/sdks/ios-meetings-sdk-screen-sharing.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

The Webex iOS Meetings SDK allows you to share the entire screen of your iOS mobile device during a call or meeting.

---

This article guides your through implementing screen sharing in your own iOS application.

## Selected section

## Broadcast Upload Extension for Screen Sharing

iOS 11 introduced a built-in screen recording and broadcast feature, allowing you to record your screen without jailbreaking or using external software. The [WWDC Video](https://developer.apple.com/videos/play/wwdc2017/606/) provides a high-level overview.

The Webex SDK transfers the screen recording data from your iOS device to other participants, which is why the broadcast upload extension is needed.

![Screen Sharing](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt9fcdfd7f2af685df/ScreenSharing.png)

An app containing one or more extensions is known as a containing app. App extensions allow you to extend functionality beyond your app into other apps or the system. The [App Extension Programming Guide](https://developer.apple.com/library/content/documentation/General/Conceptual/ExtensibilityPG/index.html) covers everything you need to know about app extensions.
