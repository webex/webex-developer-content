---
type: Excerpt
canonical_url: https://developer.webex.com/docs/build-your-first-webex-agent-workflow
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- What you will build
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/build-your-first-webex-agent-workflow). [Full Markdown](../../../../docs/build-your-first-webex-agent-workflow.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you start](002-before-you-start.md)

## Article introduction

Use VS Code with GitHub Copilot and the Webex Messaging MCP Server to inspect a test space, prepare an update, approve a single message, and verify the posted result.

## Selected section

## What you will build

You will guide an agent through a small collaboration task: turn three supplied status facts into an update for a Webex test space. The agent uses Webex tools to check the destination and verify the result. You review the destination and message before allowing the write.

The workflow is **inspect → draft → approve → post → verify**. This tutorial uses synthetic facts and an existing test space; it does not require an application deployment or a custom MCP server.
