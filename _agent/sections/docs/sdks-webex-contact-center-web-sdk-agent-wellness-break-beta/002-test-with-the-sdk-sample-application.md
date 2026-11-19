---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks-webex-contact-center-web-sdk-agent-wellness-break-beta
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Test with the SDK sample application
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks-webex-contact-center-web-sdk-agent-wellness-break-beta). [Full Markdown](../../../../docs/sdks-webex-contact-center-web-sdk-agent-wellness-break-beta.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md)

## Article introduction

Use this guide to test Agent Wellness Break with the Webex Contact Center SDK. The SDK delivers wellness events and actions. Your application presents the break, waits for active work to finish, and returns the agent to Available.

## Selected section

## Test with the SDK sample application

Use the beta sample build supplied with your invitation. Confirm that it includes the SDK version listed above before you test. The sample uses live wellness events; it does not create mock offers.

1. Sign in as the beta test agent and initialize the sample with a temporary developer access token. Do not put the token in a screenshot or test report.
2. Register the SDK, complete station login, and set the agent to **Available**. Confirm that `isWellnessBreakEnabled` is true and that the system idle code is named `WellbeingBreak`.
3. Wait for `SUGGEST_WELLNESS_BREAK`. Select **Take wellbeing break** once. Confirm that the request stays pending after HTTP acceptance. Wait for a separate `PROVIDE_WELLNESS_BREAK` approval or `WELLNESS_BREAK_NOT_ALLOWED` denial. If no decision arrives within five minutes, confirm that the sample clears the pending request and shows a timeout message.
4. After approval, confirm that the sample enters **Idle** with the `WellbeingBreak` code. It must not send a second `ACCEPTED` action for an approved manual request.
5. Test a direct `PROVIDE_WELLNESS_BREAK` offer with no request pending. Accept it and confirm that the state-change request succeeds before the sample sends `ACCEPTED`. Test **Later** and the response timeout separately; each must send only one response and leave the agent state unchanged.
6. Accept a break during an active voice or digital task. Confirm that the break timer waits for the task and required wrap-up to finish.
7. Let the break end. Confirm that the agent returns to **Available** with aux code `0`. `WellbeingBreak` must not appear as a normal selectable idle code.
8. Repeat after logout, relogin, and a connection interruption. Confirm that a new live event works and that a missed offer does not reappear.

The test passes when the request and direct-offer paths use the correct actions, the break waits for work to finish, and the agent returns to Available.
