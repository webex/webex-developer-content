---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/ios-meetings-sdk-screen-sharing
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Set the App Group
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/ios-meetings-sdk-screen-sharing). [Full Markdown](../../../../../docs/sdks/ios-meetings-sdk-screen-sharing.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

The Webex iOS Meetings SDK allows you to share the entire screen of your iOS mobile device during a call or meeting.

---

This article guides your through implementing screen sharing in your own iOS application.

## Selected section

## Set the App Group

For the screen sharing feature, the SDK uses the screen frame buffer from the iOS Broadcast Upload Extension. The only way to share data between your app and its extensions is by using an app group container.

To enable an App Group in Xcode:

1. Select your project file in Xcode.
2. Open the **Capabilities** tab on the project target page.
3. Enable the App Group capability and assign a name for both the app and its extensions.

![App Group Example](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltd0f2b41afa5d4453/AppGroupExample.png)

This [Apple Programming Guide](https://developer.apple.com/library/content/documentation/General/Conceptual/ExtensibilityPG/ExtensionScenarios.html#//apple_ref/doc/uid/TP40014214-CH21-SW6) explains how app groups work and how to use them to share data.
