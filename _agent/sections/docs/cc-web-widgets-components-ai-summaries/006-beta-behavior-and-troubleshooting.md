---
type: Excerpt
canonical_url: https://developer.webex.com/docs/cc-web-widgets-components-ai-summaries
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Beta behavior and troubleshooting
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/cc-web-widgets-components-ai-summaries). [Full Markdown](../../../../docs/cc-web-widgets-components-ai-summaries.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Add AI-generated summaries to a Webex Contact Center Widgets application so agents can share conversation context during consults and transfers and review completed interactions during wrap-up.

## Selected section

## Beta behavior and troubleshooting

- **Review generated content.** Check summaries against the conversation before sharing or completing wrap-up. Received summaries are read-only; initiating and post-call summaries support editing.
- **Received-card format.** The received-summary view requires Adaptive Card content in this Beta. Plain-text-only payloads display an unavailable state.
- **Session history.** Received-summary history can remain in memory after task cleanup. It is not persistent browser storage: logout clears it, and a page refresh does not restore it.
- **Failure handling.** A failed generation attempt can leave earlier content visible. Use manual **Retry** when offered. Summary reporting does not block valid consult, transfer, or wrap-up actions; do not assume automatic reporting retries.
- **Diagnostics.** Keep access tokens and conversation content out of logs and reports.

| Symptom | Check or recovery |
| --- | --- |
| No Summary to share | Check the pinned Widgets release, both availability gates, and the eligible task. Verify normal call controls first. |
| No received notification or content | Check the destination, exclusion choice, and completed consult or transfer. Show Cisco AI Assistant for the receiving interaction. |
| Incorrect generated content | Correct an editable summary before submission and provide feedback. |
| No suggested wrap-up reason | Select a configured reason manually; summary content and reason suggestions are independent. |
| Generation or reporting error | Record the visible error and call state without sensitive data. Retry generation if offered and check the call operation separately. |
