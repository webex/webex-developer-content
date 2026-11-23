---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/android-meetings-sdk-screen-sharing
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Start Screen Sharing
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/android-meetings-sdk-screen-sharing). [Full Markdown](../../../../../docs/sdks/android-meetings-sdk-screen-sharing.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

The Webex iOS Meetings SDK allows you to share the entire screen of your Android mobile device during a call or meeting.

---

This article guides your through implementing screen sharing in your own Android application.

## Selected section

## Start Screen Sharing

Before continuing, ensure that the call is in a `CONNECTED` status and that you are not already sharing your screen in this call, otherwise, the callback throws an error.

To start sharing your screen:

```kotlin
activeCall.startSharing(r -> Ln.d("startSharing result: " + r));
```

When initiating screen sharing for the first time, Android displays an alert dialog warning the user that the entire screen will be captured. Checking **Don't show again** prevents this dialog from appearing in the future:

![Share content warning](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt891f4bdfd9f1537e/image2018-3-21_17-23-57.png)
