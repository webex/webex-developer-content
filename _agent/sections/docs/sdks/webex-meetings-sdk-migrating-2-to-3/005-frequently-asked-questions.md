---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-meetings-sdk-migrating-2-to-3
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Frequently Asked Questions
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-meetings-sdk-migrating-2-to-3). [Full Markdown](../../../../../docs/sdks/webex-meetings-sdk-migrating-2-to-3.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article outlines the migration process for developers who are moving their Webex Web SDK applications from version 2 to version 3. It provides information on the most important changes to the SDK to aid our existing developers in making their applications compatible with SDK version 3.

## Selected section

## Frequently Asked Questions

As you prepare to upgrade, we've compiled some key questions and answers to streamline your transition. This guide will help you navigate the new features, address the breaking changes, and ensure a smooth update process. If further assistance is needed, our support team is ready to assist you.

**1. What is the Webex Web SDK V3?**

The Webex Web SDK V3 is the newest Meetings SDK launched as part of the Webex Developer Platform. It introduces various new capabilities and features.

**2. What's new in V3?**

V3 SDK introduces:

- Closed captions for live transcriptions.
- Improved background noise reduction.
- Virtual background effect supporting background blur, virtual image, and virtual video.

**3. What are the differences between V1/V2 and V3?**

Key differences include:

- Handling of local media.
- The payload for the `media:ready` event.
- Audio and video effects.
- Stream mute events and methods.
- Migration to improved meetings experience (available since V2.60.0).
- Multistream support.

**4. Will V1/V2 of the Webex Web SDK still be supported, and for how long?**

Support for the V1 SDK has ended. The V2 SDK will reach End of Life (EoL) by November 1, 2024, and will be supported until that date.

**5. Are there any tools or scripts provided to facilitate the migration process?**

Currently, no tool or script is available to assist with this migration due to the unique ways applications use the SDK.

**6. Can I run V1/V2 and V3 SDKs in parallel during the transition?**

Running V1/V2 and V3 SDKs in parallel is not advised and not supported, as this setup has not been tested.

**7. Are there any known issues or limitations in V3 that I should be aware of before migrating?**

Known limitations include:

- Screen sharing with tab audio is not supported during Transcoded meetings, but it is supported in Multistream settings.
- Screen sharing using Firefox may freeze when sharing the entire screen.

**8. What are the system and browser requirements for V3?**

- **Browser:** Compatible with all Chromium and Webkit-based browsers, including Google Chrome, Microsoft Edge, and Apple Safari.
- **NodeJS:** For the Node version of the Webex SDK, ensure your app's node versions are:
  - Node - 16.x
  - NPM - 6.x or later

**9. Are there any changes in the method signature or event payloads in V3?**

Response formats remain unchanged. However, there are request changes for:

- Method: Input changes for the `meeting.addMedia` method.
- Event: Changed payload for the `media:ready` event on the meeting object.

For more details, read the [here](https://developer.webex.com/docs/sdks/webex-meetings-sdk-migrating-2-to-3#media-event-payload-changes).

**10. What is a Transcoded meeting?**

A transcoded meeting involves the Webex cloud combining video streams from all participants into a single stream transmitted to clients.

**11. What is a Multistream meeting?**

A multistream meeting allows the Webex cloud to send individual video streams from all participants to clients, enabling customized stream layouts.

Here's the [Quick Start guide to Multistream meetings](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-multistream-quick-start).

**12. Is there any change in the licensing or pricing for the use of V3?**

Refer to the [SDK LICENSE](https://github.com/webex/webex-js-sdk/blob/next/LICENSE.md).

**13. How to avail support during and after migrating to V3?**

Reach out to the SDK team through:

- [Developer Support](https://developer.webex.com/support)
- [Developer Community](https://community.cisco.com/t5/webex-for-developers/bd-p/disc-webex-developers)
- [GitHub Repository Issues](https://github.com/webex/webex-js-sdk/issues) - (Issues, Q&A, Features)
- Email - [devsupport@webex.com](mailto:devsupport@webex.com)

These channels can also be used to report bugs in the V3 SDK.

**14. Where can I find documentation for the new V3 features?**

The Webex Meetings SDK documentation is available here: [Webex Web Meetings SDK](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-introduction).

**15. Are there any other resources?**

Additional resources include:

- **Webinar:** [Upgrade Your App with Webex Meetings SDK V3 Simplified Integration and Enhanced Features](https://app.vidcast.io/share/bcd28aa8-ab52-46bc-8ca8-3c2aa41f8f83)
- **Meetings Demo app:** Access the [source code to the demo application](https://github.com/WebexSamples/webex-js-sdk-meeting-demo/) from the webinar.
- **Vidcast:** [Kitchen Sink App Walkthrough](https://app.vidcast.io/share/e88ad798-d911-4e25-a5ba-c4f75740d2c3)
- **Kitchen Sink App:** Test various features using our [Kitchen Sink app](https://webex.github.io/webex-js-sdk/). The source code is available [here](https://github.com/webex/webex-js-sdk/tree/next/docs/samples).

**16. What is Improved Meetings Experience?**

The improved meetings experience combines **Webex Meetings** (Scheduled Webex Meetings, PMR) and **Space Meetings** (Scheduled Space Meetings, Instant Space Meetings).

Discover more about it here: [Webex App | Improved meetings associated with a space](https://help.webex.com/en-us/article/gxw5jz/Webex-App-%7C-Improved-meetings-associated-with-a-space)

**17. Does Migration to Improved Meetings Experience require only SDK upgrade?**

No, organization-level changes are also necessary for the new, improved meetings experience. Learn more about it:

- [Migrating to Improved Meetings Experience](https://developer.webex.com/docs/space-meetings-migration)
- [Web SDK: Migration to Improved Meetings Associated with a Space](https://github.com/webex/webex-js-sdk/wiki/Migration-to-improved-meetings-associated-with-a-space)

**18. When is EoL for the Old Meetings Experience?**

The EoL for the Old Meetings Experience is set for July 1, 2024. Organizations should complete their migration before this date.

**19. The EoL for Old Meetings Experience is conflicting with EoL of V2 SDK. I'm confused**

Here's a clearer timeline:

- Old Meetings Experience
  - Supported by Web SDK until **V2.60.0**
  - End of Life - July 1, 2024
- Web SDK V2
  - Supports Improved Meetings Experience from **V2.60.0**
  - End of Life - November 1, 2024

If you're planning to migrate from the Old Meetings Experience and can transition to Web SDK V3, it's recommended to migrate to V3 and the Improved Meetings Experience at the same time. If you need more time for V3, upgrade to Web SDK V2.60.0 or a later V2 version before July 1, 2024, and plan a separate migration to V3 SDK.
