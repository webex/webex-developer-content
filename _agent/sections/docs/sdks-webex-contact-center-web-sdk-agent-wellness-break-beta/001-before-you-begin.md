---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks-webex-contact-center-web-sdk-agent-wellness-break-beta
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Before you begin
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks-webex-contact-center-web-sdk-agent-wellness-break-beta). [Full Markdown](../../../../docs/sdks-webex-contact-center-web-sdk-agent-wellness-break-beta.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Use this guide to test Agent Wellness Break with the Webex Contact Center SDK. The SDK delivers wellness events and actions. Your application presents the break, waits for active work to finish, and returns the agent to Available.

## Selected section

## Before you begin

- Join the [Webex Developer Beta Program](https://developer.webex.com/docs/webex-developer-beta-program) and use an approved Contact Center organization and agent.
- Confirm that the organization has an AI Assistant entitlement and that agent wellbeing and wellness break reminders are enabled. The SDK reports the effective result as `profile.isWellnessBreakEnabled`. Your application does not need a separate wellness feature toggle.
- Use `@webex/contact-center` **3.12.0-next.133**. If your application uses the `webex` aggregate package, use **3.12.0-next.220**. Pin these package versions for this beta.
- Complete the [Webex Contact Center Web SDK Quickstart](https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-quickstart). Register the SDK and complete station login or relogin before sending a wellness action.
- Use one active agent session per SDK instance. This beta does not support multiple sessions or organizations in one instance.

Wellness events arrive through the AI Assistant real-time connection. The SDK opens that connection when the effective wellness flag is true, even if transcripts and suggested responses are disabled. A missed offer is not replayed after a connection interruption.

Watch the [SDK wellness demonstration](https://app.vidcast.io/share/aec5197c-5bbe-4d1a-b2f3-a193adb64853) for an example of the test flow.
