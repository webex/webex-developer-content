---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks-webex-contact-center-web-sdk-agent-wellness-break-beta
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Troubleshoot the test
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks-webex-contact-center-web-sdk-agent-wellness-break-beta). [Full Markdown](../../../../docs/sdks-webex-contact-center-web-sdk-agent-wellness-break-beta.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md)

## Article introduction

Use this guide to test Agent Wellness Break with the Webex Contact Center SDK. The SDK delivers wellness events and actions. Your application presents the break, waits for active work to finish, and returns the agent to Available.

## Selected section

## Troubleshoot the test

- **The feature is unavailable:** Check the AI Assistant entitlement, wellbeing and reminder settings, the SDK version, station login, and `profile.isWellnessBreakEnabled`. Register again after the organization configuration changes.
- **A request stays pending:** HTTP 202 confirms receipt only. Wait for `PROVIDE_WELLNESS_BREAK` or `WELLNESS_BREAK_NOT_ALLOWED`. If no decision arrives within five minutes, clear the pending UI without changing the agent state or sending `NO_RESPONSE`. Check that the real-time connection and active session are current; do not retry automatically.
- **A wellness action fails:** Complete station login or relogin. The action methods do not accept an agent or session override.
- **The break does not start or end:** Check the observed `WellbeingBreak` state, active tasks, wrap-up, timer, and Available restoration. Do not start a timer based on HTTP acceptance alone.
