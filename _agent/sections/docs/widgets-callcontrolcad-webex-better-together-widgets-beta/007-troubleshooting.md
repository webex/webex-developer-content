---
type: Excerpt
canonical_url: https://developer.webex.com/docs/widgets-callcontrolcad-webex-better-together-widgets-beta
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Troubleshooting
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/widgets-callcontrolcad-webex-better-together-widgets-beta). [Full Markdown](../../../../docs/widgets-callcontrolcad-webex-better-together-widgets-beta.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md) [Release scope and limitations](006-release-scope-and-limitations.md)

## Article introduction

Use this guide to test Webex Better Together with the Webex Contact Center Widgets package. Agents can handle supported voice-call actions from an embedded host application while the call runs in Webex App on the same computer.

## Selected section

## Troubleshooting

| Symptom | What to check |
| --- | --- |
| Accept, Mute, or Keypad is missing | Set `enableWxBetterTogether: true` before initialization, then initialize and log in again. |
| Accept remains disabled | Confirm the host passes the store-provided task through the `incomingTask` prop. `IncomingTask` resolves the current task from `store.taskList` by `interactionId`; use a Widgets release that includes this live task resolution behavior. |
| Mute is out of sync | Confirm the call is an engaged wxApp call, Webex App is running, both clients use the same user on the same computer, and the agent used Extension or Agent DN login. Log out and back in if needed. |
| Accept or Decline shows an inline error | Confirm Webex App is signed in and reachable and the organization is provisioned for wxApp offers. |
| A native Webex incoming toast still appears | Confirm the flag was enabled before initialization and station login completed after initialization; log out and back in. |
| Toast suppression remains stale after an embed crash | Log out and back in. Reinitialize with the flag off to clear suppression on the next login. |
| The feature works in the sample but not in production | Deploy matching `@webex/contact-center` and `@webex/cc-widgets` releases that include Webex Better Together support. |
