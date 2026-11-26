---
type: Excerpt
canonical_url: https://developer.webex.com/docs/cc-web-widgets-components-ai-summaries
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Review and share a mid-call summary
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/cc-web-widgets-components-ai-summaries). [Full Markdown](../../../../docs/cc-web-widgets-components-ai-summaries.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Add AI-generated summaries to a Webex Contact Center Widgets application so agents can share conversation context during consults and transfers and review completed interactions during wrap-up.

## Selected section

## Review and share a mid-call summary

Opening **Consult Request** or **Transfer Request** requests a summary of the conversation so far. The workflow is the same for both actions:

1. During an active voice call, open the consult or transfer action and choose an eligible destination. The examples use **Agent** and the agent search field.
2. Review **Summary to share** against the conversation. Use the edit control to correct the content, the copy control to copy it, and the thumbs controls to provide feedback.
3. To omit the summary from this submission, select **Exclude summary**. Widgets preserve the generated content and disable its edit, copy, and feedback controls while exclusion is selected. The destination remains available if it meets the normal call requirements.
4. Select **Consult** or **Transfer** to proceed, or the footer **Cancel** to leave without starting the action.

The cards illustrate fields such as **Transfer/Consult Reason**, **Details**, and **Actions taken**. Labels can vary with the returned content and renderer. Conversation text and identifying information are redacted in all screenshots.

### Consult request

Review the summary before starting the consult with the selected agent.

![Consult Request with Summary to share, copy, edit and feedback controls, Exclude summary, Cancel and Consult; identities and conversation text are redacted.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt25f685fd73b446cc/6ae462ceb706bba69c516739/cc-widgets-ai-summaries-consult.png)

### Transfer request and editing

Review and correct the content before transferring. The edit view displays **Editing** and the editable summary fields.

![Transfer Request with Summary to share, summary controls, Exclude summary, Cancel and Transfer; conversation text is redacted.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt646aa6fea1e5d046/6ae462c3084ab9ef7ee35fb7/cc-widgets-ai-summaries-transfer.png)

![Transfer Request in Editing state with editable summary fields, feedback and exclusion controls; conversation text is redacted.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt3c556f4abe152ac1/6ae4630d0ac6661fc6d2fdb0/cc-widgets-ai-summaries-edit.png)

The dialog may also list Queue, Dial Number, and Entry Point destinations. Their availability follows the underlying call flow; summary delivery can differ by destination.

Consult and transfer remain subject to their normal task-state and destination checks. Summary reporting is handled independently of the call operation, and an unavailable summary does not prevent an otherwise valid call action. If generation fails, use **Retry** when offered. Closing the dialog does not cancel an already active call operation.
