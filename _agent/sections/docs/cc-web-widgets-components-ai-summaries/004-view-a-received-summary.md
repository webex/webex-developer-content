---
type: Excerpt
canonical_url: https://developer.webex.com/docs/cc-web-widgets-components-ai-summaries
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- View a received summary
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/cc-web-widgets-components-ai-summaries). [Full Markdown](../../../../docs/cc-web-widgets-components-ai-summaries.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Add AI-generated summaries to a Webex Contact Center Widgets application so agents can share conversation context during consults and transfers and review completed interactions during wrap-up.

## Selected section

## View a received summary

The receiving agent can view shared content without requesting another summary:

1. Receive the consult or transfer.
2. When **Transfer summary available** appears, select **View summary** to open Cisco AI Assistant, or **Later** to dismiss the notification. If the assistant is already open, review the summary there.
3. Review the received context. Received cards are read-only; use their copy and feedback controls as needed.
4. After choosing **Later**, reopen or restore Cisco AI Assistant during the interaction to view the retained summary.

![Cisco AI Assistant displaying a received mid-call summary with copy and feedback controls; sender identity, timestamp and conversation text are redacted.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt985b73a4399746a0/6ae463383ab81bbf97fbe473/cc-widgets-ai-summaries-received.png)

**Later** dismisses the notification without discarding the summary. The panel displays summaries for the current interaction. Widgets keep received cards associated with their originating interaction and handle card-specific feedback. A failed feedback submission preserves the previous selection and does not prevent viewing the summary.
