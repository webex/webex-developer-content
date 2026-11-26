---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-participant-drop-sdk-beta
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Troubleshooting and feedback
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-participant-drop-sdk-beta). [Full Markdown](../../../../../docs/sdks/webex-contact-center-web-sdk-participant-drop-sdk-beta.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md)

## Article introduction

Participant Drop lets the primary agent remove an eligible participant from an active Webex Contact Center voice conference. Use the voice task's `dropConferenceParticipant` method, then refresh your application from the updated task rather than removing a participant from the UI immediately.

## Selected section

## Troubleshooting and feedback

If Drop is unavailable, check that the task is an active voice conference, the current agent is the backend-selected primary owner, the target has joined the main conference, and the organization is enabled. For a rejected request, wait for it to settle before retrying; do not infer success from the button click.

Report the scenario, expected and actual result, approximate time and time zone, browser, operating system, SDK build, and whether the agent was primary or secondary. Include a non-sensitive tracking reference if available. Do not send access tokens, credentials, names, full phone numbers, participant identifiers, authorization headers, request URLs, or raw routing payloads.
