---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-connect-ai-skills-and-plugin
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Overview
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webex-connect-ai-skills-and-plugin). [Full Markdown](../../../../docs/webex-connect-ai-skills-and-plugin.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](002-before-you-begin.md) [MCP endpoints, region, and authentication](009-mcp-endpoints-region-and-authentication.md)

## Article introduction

Install and use Webex Connect AI Skills with Codex, Claude Code, Cursor, or standalone skill packages. This guide explains the 19 available skills, plugin and skill installation, tenant and credential prerequisites, common workflows, MCP setup, and production safeguards.

## Selected section

## Overview

Webex Connect skills are focused instruction packages that help an AI coding agent build, configure, and operate Webex Connect workflows. They explain when a workflow applies, what information it needs, how to validate the request, and how to handle the result.

The public Webex Skills repository provides two ways to install these instructions:

- **Standalone skills** install selected workflows individually.
- **Webex Connect AI plugin** bundles the Connect skills with host-specific commands, rules, manifests, and branding.

The plugin includes 19 independently packaged skills. The source repository currently identifies the plugin as a beta release. The skill set and versions can change; the table below reflects the current catalog.

Installing a skill or plugin does not create a Webex Connect tenant, register a mobile device, approve a sender, configure credentials, or enable an MCP connection. Complete the relevant setup steps in this guide before using API-backed workflows.
