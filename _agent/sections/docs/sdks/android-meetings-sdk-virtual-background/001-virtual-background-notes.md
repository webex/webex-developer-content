---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/android-meetings-sdk-virtual-background
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Virtual Background Notes
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/android-meetings-sdk-virtual-background). [Full Markdown](../../../../../docs/sdks/android-meetings-sdk-virtual-background.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Enhance your video appearance and maintain professionalism, privacy, and focus by using a virtual background in meetings.

---

This article describes how you can use the Webex Android Meetings SDK to work with virtual backgrounds in your app.

## Selected section

## Virtual Background Notes

When using custom virtual backgrounds, consider the following guidelines:

- Supported image formats for custom backgrounds are JPG and PNG.
- The SDK resizes images larger than 1280x720 to avoid excessive CPU usage.
- Application storage will increase based on the custom images used.
- High CPU usage by the Virtual Background feature may trigger `CallObserver.onCpuHitThreshold()`. If that happens, consider disabling the feature.
