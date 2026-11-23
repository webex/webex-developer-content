---
type: Excerpt
canonical_url: https://developer.webex.com/docs/cc-web-widgets-components-ai-summaries
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Review a post-call summary
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/cc-web-widgets-components-ai-summaries). [Full Markdown](../../../../docs/cc-web-widgets-components-ai-summaries.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Add AI-generated summaries to a Webex Contact Center Widgets application so agents can share conversation context during consults and transfers and review completed interactions during wrap-up.

## Selected section

## Review a post-call summary

During wrap-up, **Wrap Up Reasons** displays **Summary of your conversation** beside the configured reason selector:

1. End the call and open **Wrap Up Reasons**.
2. Review the summary, correct editable content, and copy it or provide feedback as needed.
3. Choose a valid configured reason in **Search topic**. If an AI-suggested reason is available, review it and select the matching configured reason, or choose another manually.
4. Select **Submit Wrap Up** to complete wrap-up. Selecting a suggestion alone does not submit it.

![Wrap Up Reasons with Search topic, No suggestion available, Summary of your conversation, summary controls and Submit Wrap Up; conversation text is redacted.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt3345620941bbd266/6ae4636fd777730bfcfb39d0/cc-widgets-ai-summaries-wrap-up.png)

A summary can be available without a suggested reason. When **AI-suggested: No suggestion available** appears, or a suggestion has no valid configured match, select a configured reason manually.

Summary generation and reason selection are independent. A valid selected reason can keep **Submit Wrap Up** available while generation is pending. Widgets report the selected code identifier and complete task wrap-up separately, without waiting for summary-reporting acknowledgement.
