---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/ai-summaries
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Beta overview
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/ai-summaries). [Full Markdown](../../../../../docs/sdks/ai-summaries.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](002-before-you-begin.md) [Beta limitations and error handling](007-beta-limitations-and-error-handling.md)

## Article introduction

Add AI-generated summaries to a Webex Contact Center SDK application so agents can share conversation context during consults and transfers and review completed interactions during wrap-up.

## Selected section

## Beta overview

AI Summaries Beta is available in `@webex/contact-center@3.12.0-next.159` and supports two workflows:

| Workflow | Agent experience |
| --- | --- |
| Mid-call summary | Generate and review a summary before an agent-to-agent consult or transfer. The receiving agent can view the shared summary. |
| Post-call summary | Review and edit a summary during wrap-up, with suggested wrap-up reasons when available. |

The SDK provides summary generation, response reporting, capability updates, and an event for received mid-call summaries. Your application provides the review UI, editing, notifications, feedback, and usage tracking. Consult, transfer, and task wrap-up use their existing task APIs.
