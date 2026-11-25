---
type: Excerpt
canonical_url: https://developer.webex.com/docs/embedded-apps-for-webex-devices
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Optimizing the Experience for Webex Devices
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/embedded-apps-for-webex-devices). [Full Markdown](../../../../docs/embedded-apps-for-webex-devices.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Technical Requirements and Limitations](007-technical-requirements-and-limitations.md) [Requirements for Embedded Apps on Devices](008-requirements-for-embedded-apps-on-devices.md)

## Selected section

## Optimizing the Experience for Webex Devices

Embedded apps can check the value of [webex.application.deviceType](https://developer.webex.com/docs/embedded-apps-api-reference#Webex.Application+deviceType) in the Embedded App SDK to see what type of device the application is running on. This property currently returns the string `"ROOM_SYSTEM_PERSONAL"` when running on a Webex Device. Information about the exact device model can be found in the [webex.application.about](https://developer.webex.com/docs/embedded-apps-api-reference#Webex.Application+about) property. This makes it possible to adapt the functionality of your app specifically for the Webex Device, if needed.
