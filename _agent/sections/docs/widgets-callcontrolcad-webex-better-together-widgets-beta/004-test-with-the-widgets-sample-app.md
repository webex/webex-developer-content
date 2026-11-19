---
type: Excerpt
canonical_url: https://developer.webex.com/docs/widgets-callcontrolcad-webex-better-together-widgets-beta
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Test with the Widgets sample app
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/widgets-callcontrolcad-webex-better-together-widgets-beta). [Full Markdown](../../../../docs/widgets-callcontrolcad-webex-better-together-widgets-beta.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md) [Release scope and limitations](006-release-scope-and-limitations.md)

## Article introduction

Use this guide to test Webex Better Together with the Webex Contact Center Widgets package. Agents can handle supported voice-call actions from an embedded host application while the call runs in Webex App on the same computer.

## Selected section

## Test with the Widgets sample app

Use the Contact Center Widgets sample app from the Widgets repository and keep Webex App desktop open on the same computer, signed in as the test agent.

1. Open the sample app and authenticate as the test agent.
2. Before initializing widgets, enable **Answer on Webex** in **SDK Toggles**. This sets `webexConfig.cc.enableWxBetterTogether`.

   ![SDK Toggles with Answer on Webex enabled](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt7442abce6c38419d/6abe423bfcb9ad705c2b14d9/webex-better-together-widgets-setup.png)
3. Initialize the widgets and confirm there are no errors.
4. Select `IncomingTask`, `TaskList`, and `CallControl` in the widget picker.
5. Log in with an Extension or Agent DN and set the agent state to Available.
6. Start an inbound wxApp voice interaction. Confirm the offer displays **Accept** and **Decline** in `IncomingTask` or `TaskList`.

   ![Incoming task card with Accept and Decline actions](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt1ebe47578b88682d/6abe43248aebed7ab2dca83b/webex-better-together-widgets-incoming-task.png)
7. Accept the task and confirm the call engages in Webex App desktop.
8. Confirm `CallControl` displays **Mute** and **Keypad** during the engaged call.

   ![Call controls showing Mute and Keypad during an active call](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt088dd865a202ee3f/6abe43c0ec9eb7e00569d3d4/webex-better-together-widgets-call-control.png)
9. Mute in the embed and confirm the Webex App microphone state matches. Optionally mute or unmute in Webex App and confirm the embed updates.

   ![Mute control reflecting the synchronized call mute state](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt7c75e525a4a36f19/6abe445bfc9e37d19428c78c/webex-better-together-widgets-mute-control.png)
10. Send keypad digits and confirm the IVR receives the tones.

   ![Dialpad and DTMF controls displayed during an active call](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt6ca148cfd9c16523/6abe455ef5361482690df19c/webex-better-together-widgets-dialpad.png)
11. End and wrap up the active task, then set the agent state to Available. Start a fresh inbound wxApp voice interaction and, while its offer is pending, cause an Accept or Decline failure, such as by making Webex App unavailable. Confirm an inline error appears on the offer card. Restore Webex App and accept the pending offer before continuing to step 12.

   ![Incoming task card showing the unable-to-answer error and retry message](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt3e638f63e20b8b08/6abe45a8e2bfa6b505f4d590/webex-better-together-widgets-error-state.png)
12. End the task and confirm the offer state clears.
