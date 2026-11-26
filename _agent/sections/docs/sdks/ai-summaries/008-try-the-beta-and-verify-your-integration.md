---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/ai-summaries
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Try the Beta and verify your integration
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/ai-summaries). [Full Markdown](../../../../../docs/sdks/ai-summaries.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](002-before-you-begin.md) [Beta limitations and error handling](007-beta-limitations-and-error-handling.md)

## Article introduction

Add AI-generated summaries to a Webex Contact Center SDK application so agents can share conversation context during consults and transfers and review completed interactions during wrap-up.

## Selected section

## Try the Beta and verify your integration

Use the [Contact Center SDK sample](https://web-sdk.webex.com/samples/contact-center/) with an eligible test tenant, an authorized caller, two eligible agent sessions for consult and transfer, and a configured wrap-up reason. The hosted sample's deployed SDK version can differ from this guide's pinned Beta; check its build before testing.

In **Auth & Registration**, choose the environment and SDK toggles, supply an authorized test agent's access token, select **webex.init()**, then **webex.cc.register()**, and wait for completion. In **Agent Station Login/Logout**, select a permitted team and station option, select **Login**, and set the agent to Available.

Watch [sdk ai summaries — 1 minute 34 seconds](https://app.vidcast.io/share/cf7c0bc6-1dd5-4ae1-aabe-f1438a98d1e3), by Ravi Chandra Sekhar Sarika, for a walkthrough of consult-summary generation, receiving-agent display, and post-call review, editing, feedback, and wrap-up. Your application must invoke the generation methods; binding listeners alone does not generate summaries.

Validate the following in your configured Beta environment. Record the SDK build, setup, and observed result, then complete the test calls and session cleanup.

| Area | Verify |
| --- | --- |
| Availability and lifecycle | Controls reflect both the initial capability snapshot and updates. New and restored tasks have listeners; task changes do not display stale results. |
| Consult and transfer | Both actions generate content, preserve reviewed edits, and report with the matching action. Verify the call operation and receiving-agent content separately. |
| Review and feedback | View, edit, and copy counts reflect agent actions. Exclusion, cancellation, and receiving-card feedback use the intended response or event values. |
| Post-call wrap-up | Reporting and wrap-up complete independently. Suggested reasons map to configured codes, and manual selection works without suggestions. |
| Content and failures | Handle structured text, plain text, supported cards, and missing content. Test disabled features, timeouts, duplicate submissions, and session changes during pending work. |
