---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-connect-ai-skills-and-plugin
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Complete the task
- Example requests
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webex-connect-ai-skills-and-plugin). [Full Markdown](../../../../docs/webex-connect-ai-skills-and-plugin.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](002-before-you-begin.md) [MCP endpoints, region, and authentication](009-mcp-endpoints-region-and-authentication.md)

## Article introduction

Install and use Webex Connect AI Skills with Codex, Claude Code, Cursor, or standalone skill packages. This guide explains the 19 available skills, plugin and skill installation, tenant and credential prerequisites, common workflows, MCP setup, and production safeguards.

## Parent context

## Complete the task

## Selected section

### Example requests

**Send an SMS**

> Use the Webex Connect SMS skill to prepare an approved utility SMS to my test recipient with the configured sender ID. Show me the recipient and message before sending.

The workflow validates the E.164 recipient, sender, encoding, and Send Message API v2 request. It reports acceptance and the message ID; acceptance does not prove delivery.

**Send an Email through MCP**

> Use the Webex Connect Email skill. Find the approved sender for this use case, show me the sender and recipient, and wait for my confirmation before sending.

The MCP path must already be configured. If sender discovery finds no compatible sender, ask an administrator to approve one; do not invent a sender ID.

**Manage a digital asset**

> Create a Webex Connect digital asset.

For retrieval or update, name the operation and provide the documented asset identifier. The skill asks which operation and asset type apply, validates against that operation's schema, and requests confirmation before a create or update.

**Build a widget or mobile integration**

> Use the Webex Connect Live Chat widget skill to build a browser widget for my tenant.

For mobile work, select the Android or iOS Push and In-App Messaging builder. These builders collect app identifiers and platform credentials, then produce an integration structure with validation and QA steps.

**Test in Sandbox**

Use the Sandbox skill for supported SMS, Voice, or WhatsApp tests. Sandbox setup must not configure the Production CPaaS MCP server or its credentials.
