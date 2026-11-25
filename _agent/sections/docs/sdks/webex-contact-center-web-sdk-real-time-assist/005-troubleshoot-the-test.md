---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-real-time-assist
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Troubleshoot the test
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-real-time-assist). [Full Markdown](../../../../../docs/sdks/webex-contact-center-web-sdk-real-time-assist.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md)

## Article introduction

Use this guide to test Real Time Assist with the Webex Contact Center SDK. Start with the sample application, then add the request, response, and feedback handling to your application.

## Selected section

## Troubleshoot the test

- **The request returns a feature-disabled error:** Confirm that Real Time Assist is enabled for both the organization and the agent profile.
- **The request succeeds but no response event arrives:** Confirm that the listener is attached to the current task before the request and that the interaction is still active.
- **Feedback fails:** Confirm that the `interactionId` belongs to the current task and that `adaptiveCardId` came from the response whose control the agent selected.
- **A response appears under the wrong customer:** Clear your rendered responses when the task ends and keep response state separate for each interaction.
