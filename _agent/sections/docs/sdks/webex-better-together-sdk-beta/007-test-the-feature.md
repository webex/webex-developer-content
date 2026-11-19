---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-better-together-sdk-beta
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Test the feature
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-better-together-sdk-beta). [Full Markdown](../../../../../docs/sdks/webex-better-together-sdk-beta.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Overview and limitations](001-overview-and-limitations.md) [Before you begin](002-before-you-begin.md)

## Article introduction

Use this guide to integrate and test Webex Better Together with the Webex Contact Center SDK. It lets an agent use a host application for call controls while the voice call runs in Webex App on the same computer.

## Selected section

## Test the feature

Keep Webex App desktop open on the same computer as the host application and use an organization provisioned for wxApp telephony.

[Watch the SDK sample walkthrough — Answer, Mute, and Keypad (Vidcast, 4m 33s)](https://app.vidcast.io/share/02dd6537-fb8c-4604-b9d1-ef6816f91803)

### Test with the SDK sample app

Use the [Webex Contact Center SDK sample app](https://webex.github.io/webex-js-sdk/samples/contact-center/) to register, log in with an Extension or Agent DN, and set the agent to Available.

1. Start an inbound Webex App voice offer and confirm **Accept** and **Decline** appear.
2. Accept the offer and confirm the call engages in Webex App.
3. Mute in the sample app and confirm the Webex App microphone mutes. Unmute in Webex App and confirm the host mute icon updates.
4. Refresh during the engaged call and confirm mute state is restored from call details.
5. Send keypad digits and confirm they reach the IVR.
6. After ending and wrapping up the active task, create an outbound ringing offer and confirm **Decline** clears it.

### Test with your host application

1. Initialize with `enableWxBetterTogether: true`, await SDK readiness, then register and complete Extension or Agent DN station login.
2. Bind incoming and hydrated tasks to the host UI and refresh controls on `task:ui-controls-updated`.
3. Wire guarded Accept/Decline handlers to the offered task.
4. When the task becomes the active engaged call, attach its mute listener and seed mute state. Wire Mute and Keypad to that task.
5. Set the agent to Available, create an inbound offer, and verify acceptance, mute in both directions, keypad entry, and refresh/reconnect recovery.
6. End and wrap up using the existing task methods. Confirm host listeners are detached on task end or host removal, and only one client answers each offer.

For existing hold, transfer, consult, end, and wrap-up behavior, follow [Webex Contact Center SDK Tasks](https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-tasks).
