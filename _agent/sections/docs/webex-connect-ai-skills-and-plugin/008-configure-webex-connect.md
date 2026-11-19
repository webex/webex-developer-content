---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-connect-ai-skills-and-plugin
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Complete the task
- Configure Webex Connect
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webex-connect-ai-skills-and-plugin). [Full Markdown](../../../../docs/webex-connect-ai-skills-and-plugin.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](002-before-you-begin.md) [MCP endpoints, region, and authentication](009-mcp-endpoints-region-and-authentication.md)

## Article introduction

Install and use Webex Connect AI Skills with Codex, Claude Code, Cursor, or standalone skill packages. This guide explains the 19 available skills, plugin and skill installation, tenant and credential prerequisites, common workflows, MCP setup, and production safeguards.

## Parent context

## Complete the task

## Selected section

### Configure Webex Connect

Open the application project in the AI host. For API-backed work, run the setup skill when tenant, region, authentication, or channel configuration is missing:

```text
Use webex-connect-setup to configure Webex Connect.
```

The setup flow:

1. Asks you to select Sandbox or Production. It does not silently choose an environment.
2. Collects the tenant context and confirms the region. It uses documented API hosts for each API family rather than deriving one host from another.
3. For Production, registers the region-matched SMS and Email MCP endpoint with the active AI host. Sandbox has no MCP endpoint and does not configure Production MCP.
4. Creates or updates the project `.env` with supported Messaging v1/v2, Voice, Contact Policy, Profile, Audit Logs, Digital Asset, and Production MCP endpoints. Existing values are preserved, missing keys are added, and file permissions are restricted. Credentials are left blank for you to enter locally.
5. Identifies the authentication required by the selected workflow and checks for the endpoint and credential values before an API-backed skill continues.
6. Confirms channel resources and summarizes the requested action before a send or asset mutation.

Android, iOS, and browser widget builders collect their SDK configuration directly and do not require the API `.env` preflight.

The project `.env` is not automatically loaded by every MCP host. The current setup utility registers only Production-region MCP endpoints; it does not configure Integration staging or preproduction endpoints. For staging or preproduction, manually configure the AI host's MCP server URL using the matching endpoint in the following table instead of using the Production MCP installer. Configure authentication separately using the host's documented flow. Codex uses a WCIT bearer token, Cursor supports WCIT or OAuth, and Claude Code uses browser OAuth. Do not assume that writing `.env` authenticates a remote MCP connection.
