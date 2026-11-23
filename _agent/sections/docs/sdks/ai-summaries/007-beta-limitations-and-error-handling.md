---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/ai-summaries
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Beta limitations and error handling
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/ai-summaries). [Full Markdown](../../../../../docs/sdks/ai-summaries.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](002-before-you-begin.md)

## Article introduction

Add AI-generated summaries to a Webex Contact Center SDK application so agents can share conversation context during consults and transfers and review completed interactions during wrap-up.

## Selected section

## Beta limitations and error handling

- **Concurrent operations:** Allow one pending mid-call generation request per conversation, shared across consult and transfer actions, and one pending post-call request. Prevent duplicate reports while a submission is pending. Restore controls after success or failure.
- **Cancellation and lifecycle:** There is no dedicated public summary-request cancellation method. Remove listeners when their view is released, and ignore late results after the task changes or the session ends. Manage displayed content and retained history explicitly, and clear conversation content on logout.
- **Retries:** Handle generation and reporting rejections explicitly. A failed refresh can leave previously displayed content available. Offer a user-triggered generation retry without overlapping requests; do not assume automatic reporting retries.
- **Inputs and diagnostics:** Validate caller-supplied actions and response values. Treat rejected values as `unknown`, since not every error contains `data.errorCode`. Keep tokens and conversation content out of diagnostics.

| Symptom or error | Recovery |
| --- | --- |
| `MID_CALL_SUMMARY_DISABLED` or `POST_CALL_SUMMARY_DISABLED` | Check both the organization flag and task capability. |
| `MID_CALL_SUMMARY_TIMEOUT` or `POST_CALL_SUMMARY_TIMEOUT` | Show the failure state, restore controls, and offer a manual generation retry where appropriate. |
| `AI_ASSISTANT_BASE_URL_NOT_AVAILABLE` | Check registration, environment configuration, and AI Assistant availability with the environment owner. |
| Task removal or session end during a request | Handle rejection and discard results that no longer belong to the active interaction. |
| No summary on the receiving agent | Check the destination, summary inclusion, completed consult or transfer, receiving task, and listener binding. Generation success alone does not confirm delivery. |
| Other generation or reporting failure | Handle the rejection independently of call control and record a diagnostic without credentials or summary content. |
