---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-connect-ai-skills-and-plugin
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Complete the task
- Common use cases
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webex-connect-ai-skills-and-plugin). [Full Markdown](../../../../docs/webex-connect-ai-skills-and-plugin.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](002-before-you-begin.md) [MCP endpoints, region, and authentication](009-mcp-endpoints-region-and-authentication.md)

## Article introduction

Install and use Webex Connect AI Skills with Codex, Claude Code, Cursor, or standalone skill packages. This guide explains the 19 available skills, plugin and skill installation, tenant and credential prerequisites, common workflows, MCP setup, and production safeguards.

## Parent context

## Complete the task

## Selected section

### Common use cases

| Use case | Skills to start with | Example |
| --- | --- | --- |
| Transactional or marketing messages | `webexconnect-sendmessage`, a channel-specific send skill, and `webexconnect-contact-policy` when consent rules apply | Send an approved order update, reminder, or campaign using the right channel and sender. |
| Digital-channel onboarding | `webexconnect-digital-asset-creation` | Create, retrieve, or update a Chat, Email, Facebook Messenger, or WhatsApp asset. |
| Customer support and live engagement | `webexconnect-livechat-widget` or `webexconnect-livechat-inapp-sendmessage` | Build a browser widget or support threaded Live Chat and In-App conversations. |
| Mobile engagement | Android or iOS Push and In-App Messaging builder; `webexconnect-push-sendmessage` | Build a mobile sample or send to a registered user or device. |
| Delivery operations | `webexconnect-webhooks-events` and the relevant channel skill | Process inbound events, delivery receipts, failures, callbacks, and retries. |
| Prototyping | `webexconnect-sandbox` | Test supported SMS, Voice, or WhatsApp flows with verified recipients and Sandbox limits. |
