---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/ai-summaries
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Before you begin
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/ai-summaries). [Full Markdown](../../../../../docs/sdks/ai-summaries.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Beta limitations and error handling](007-beta-limitations-and-error-handling.md)

## Article introduction

Add AI-generated summaries to a Webex Contact Center SDK application so agents can share conversation context during consults and transfers and review completed interactions during wrap-up.

## Selected section

## Before you begin

- **Configure AI Assistant.** An administrator must enable AI Assistant access and the required summary features for the applicable queues. See [Enable AI Assistant features in Control Hub for Webex Contact Center](https://help.webex.com/article/n9lk3t6/Enable-Cisco-AI-Assistant-for-Contact-Center) for licensing, user-profile, and recording prerequisites. Its Agent Desktop layout and notification instructions apply to Agent Desktop; SDK applications provide their own UI.
- **Check language availability.** See the **Supported languages for Summaries** table in [Multi-language Support for AI Assistant Features](https://help.webex.com/article/nlm6pob/Multi-language-Support-for-AI-Assistant-Features). Availability depends on the feature, locale, and SKU.
- **Initialize an agent session.** Complete authentication, SDK initialization and readiness, registration, and station login. See [Quickstart](https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-quickstart) and [Authentication](https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-authentication). Use the pinned Beta package below in place of the Quickstart's unversioned installation command.
- **Obtain the agent's task.** Follow the [task lifecycle](https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-tasks) to obtain an `ITask` for new and restored interactions. The examples in this guide begin with an initialized session and an existing task.

Install the Beta package with npm or Yarn:

```bash
npm install @webex/contact-center@3.12.0-next.159
# Alternative
yarn add @webex/contact-center@3.12.0-next.159
```
