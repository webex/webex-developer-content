---
type: Excerpt
canonical_url: https://developer.webex.com/docs/cc-web-widgets-components-ai-summaries
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Try the Beta and verify your integration
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/cc-web-widgets-components-ai-summaries). [Full Markdown](../../../../docs/cc-web-widgets-components-ai-summaries.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Add AI-generated summaries to a Webex Contact Center Widgets application so agents can share conversation context during consults and transfers and review completed interactions during wrap-up.

## Selected section

## Try the Beta and verify your integration

Use the [Contact Center Widgets React sample](https://widgets.webex.com/samples-cc-react-app/index.html) with an authorized test environment, a caller, two eligible agent sessions, and configured wrap-up reasons. Initialize it with the test agent's access token. In **Select Widgets to Show**, enable **AI Assistant**, which is not selected by default, and the station-login, agent-state, incoming-task, and call-control surfaces. Check the sample's deployed version; it can differ from this guide's pinned Beta.

Watch [Agent Handoff and post call summaries](https://app.vidcast.io/share/9b04e255-997b-4e73-94ea-dfe03acdefb3) (1 minute 55 seconds), by Ravi Chandra Sekhar Sarika, for a demonstration of mid-call review, receiving-agent context, and post-call wrap-up.

Run the following checks in your host application. Record the build, configuration, and observed results, then complete the test calls and session cleanup.

| Area | Verify |
| --- | --- |
| Setup and availability | Initialize the shared store, log in, accept a call, and confirm each summary flow follows its organization and task gates. |
| Consult and transfer | Review and edit content, complete each call action, and verify received content separately. Exercise exclusion and cancellation. |
| Received summaries | Open content with **View summary**, defer with **Later**, then reopen it. Check read-only display, copy, and card-specific feedback. |
| Post-call wrap-up | Edit the summary and submit a valid reason. Confirm suggestions require agent selection and manual reasons remain usable without suggestions. |
| Failures and session lifecycle | Exercise missing content, generation failure, and **Retry**. Check that new interactions do not show unrelated summaries and logout clears summary state. |
