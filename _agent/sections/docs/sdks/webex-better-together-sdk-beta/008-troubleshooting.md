---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-better-together-sdk-beta
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Troubleshooting
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-better-together-sdk-beta). [Full Markdown](../../../../../docs/sdks/webex-better-together-sdk-beta.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Overview and limitations](001-overview-and-limitations.md) [Before you begin](002-before-you-begin.md)

## Article introduction

Use this guide to integrate and test Webex Better Together with the Webex Contact Center SDK. It lets an agent use a host application for call controls while the voice call runs in Webex App on the same computer.

## Selected section

## Troubleshooting

| Symptom | What to check |
| --- | --- |
| Accept, Mute, or Keypad is missing | Reinitialize with `enableWxBetterTogether: true`, then register and log in again. |
| Accept remains disabled | Refresh the task from the SDK task manager and listen for `task:ui-controls-updated`; keep a visible disabled button rendered. |
| Mute is out of sync | Confirm an engaged wxApp call, Webex App running, the same user and computer, and Extension or Agent DN login. Await mute backfill; log out and back in if needed. |
| Accept, Decline, Mute, or Keypad reports an error | Display the error in the host UI. Check Webex App connectivity and organization provisioning; retry only while the control is enabled. |
| A native Webex incoming toast still appears | Confirm the flag was enabled before initialization and station login completed after initialization; log out and back in. |
| The feature works in the sample but not in the host app | Confirm the host uses `@webex/contact-center@3.12.0-next.131` and the same initialization and station-login flow. |
