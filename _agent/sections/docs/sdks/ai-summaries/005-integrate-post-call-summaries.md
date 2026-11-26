---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/ai-summaries
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Integrate post-call summaries
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/ai-summaries). [Full Markdown](../../../../../docs/sdks/ai-summaries.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](002-before-you-begin.md) [Beta limitations and error handling](007-beta-limitations-and-error-handling.md)

## Article introduction

Add AI-generated summaries to a Webex Contact Center SDK application so agents can share conversation context during consults and transfers and review completed interactions during wrap-up.

## Selected section

## Integrate post-call summaries

Request a post-call summary on the task being wrapped up:

1. Check `task.aiSummaryCapabilities.postCallEnabled`, then await `task.requestPostCallSummary()`.
2. Display the returned `AISummary`. Let the agent review and edit it, record feedback and usage, and select a configured wrap-up reason.
3. Build an `AISummaryResponse`. If reporting the selected reason, set the optional `response.wrapUpCode` to its configured code identifier (`auxCodeId`).
4. Dispatch `task.sendPostCallSummaryResponse(response)` before task cleanup and handle its result.
5. Complete wrap-up separately with `task.wrapup({wrapUpReason, auxCodeId})`, using the selected reason's label and configured identifier.

Wrap-up can start without waiting for summary-reporting acknowledgement. Handle both results independently, including when your application performs automatic wrap-up. Post-call summaries are returned by the request promise; there is no post-call-summary-received task event.

### Use suggested wrap-up reasons

`summary.suggestedWrapUpCodes` optionally contains suggested reasons, and `summary.suggestedWrapUpCodesMessage` optionally provides explanatory text. Each suggestion declares a `name`; it may not contain a configured code identifier. Match the suggestion to a valid configured reason before using it.

Suggestions do not select a reason or complete wrap-up automatically. Keep manual reason selection available when suggestions are absent or have no configured match. Summary content and wrap-up suggestions can be available independently.
