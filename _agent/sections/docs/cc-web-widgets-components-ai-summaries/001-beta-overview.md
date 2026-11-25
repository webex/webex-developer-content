---
type: Excerpt
canonical_url: https://developer.webex.com/docs/cc-web-widgets-components-ai-summaries
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Beta overview
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/cc-web-widgets-components-ai-summaries). [Full Markdown](../../../../docs/cc-web-widgets-components-ai-summaries.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Add AI-generated summaries to a Webex Contact Center Widgets application so agents can share conversation context during consults and transfers and review completed interactions during wrap-up.

## Selected section

## Beta overview

AI Summaries Beta is available in `@webex/cc-widgets@1.28.0-next.66`, which uses Contact Center SDK `3.12.0-next.159` through its store dependency.

| Workflow | Widget experience |
| --- | --- |
| Mid-call consult or transfer | Agents review, edit, and share a summary from the call controls. They can also exclude it from the submission. |
| Received summary | The receiving agent views read-only conversation context in **Cisco AI Assistant**, with copy and feedback controls. |
| Post-call wrap-up | Agents review and edit the completed conversation summary alongside configured wrap-up reasons. |

This guide covers agent-to-agent voice calls. AI Agent transfer summaries and dropped-call summaries are separate features. Widgets manage summary generation, presentation, editing, feedback, and response reporting; host applications using these controls should not issue duplicate SDK summary requests.
