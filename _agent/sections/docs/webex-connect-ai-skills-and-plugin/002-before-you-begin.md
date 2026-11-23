---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-connect-ai-skills-and-plugin
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Before you begin
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webex-connect-ai-skills-and-plugin). [Full Markdown](../../../../docs/webex-connect-ai-skills-and-plugin.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [MCP endpoints, region, and authentication](009-mcp-endpoints-region-and-authentication.md)

## Article introduction

Install and use Webex Connect AI Skills with Codex, Claude Code, Cursor, or standalone skill packages. This guide explains the 19 available skills, plugin and skill installation, tenant and credential prerequisites, common workflows, MCP setup, and production safeguards.

## Selected section

## Before you begin

### AI host and installation tools

- The plugin supports Codex, Claude Code, and Cursor.
- Standalone installers also support GitHub Copilot. Client support can vary by skill; check the skill's entry in the catalog.
- For repository-based plugin installation, install Git and make sure the host can access GitHub.
- Standalone skill installers use Node.js 20 or later and npm (which provides `npx`). Setup utilities use Python 3.
- The shell commands below use macOS or Linux paths. On Windows, use the equivalent paths and copy commands for your host.

### Webex Connect tenant and credentials

Have access to a Webex Connect tenant and decide whether the task uses Sandbox or Production. Gather only the credentials required by the selected workflow.

| Workflow | Required access or credential |
| --- | --- |
| Messaging, Event, Voice, or inbound webhook APIs | Service Key or the service-specific JWT |
| Profile and Contact Policy APIs | Profile Key |
| Digital Asset API | Webex personal access token, organization ID, and the Digital Channel Onboarding API host |
| SMS or Email through MCP with Codex | Webex Client Integration Token (WCIT) with the `spark:mcp` scope. Additional tool scopes are requested at runtime through MCP elicitation; protect the local Codex configuration that contains the bearer token. |
| SMS or Email through MCP with Cursor | WCIT with the `spark:mcp` scope using token-based authentication, or OAuth through an Integration App with Cursor's fixed redirect URI `cursor://anysphere.cursor-mcp/oauth/callback`. |
| SMS, Email, or sender discovery through Claude Code | Integration App client ID and client secret, plus a registered callback URI (for example, `http://localhost:PORT/callback`) and matching callback port. Complete browser authentication after adding the MCP server. See the [Claude Code MCP setup guide](https://developer.webex.com/docs/webex-agentic-mcp-servers-claude-code). |
| Webhook signature verification | Configured Hub Secret |

Prepare channel resources where the task needs them:

- **SMS or Email:** an approved sender and recipient details.
- **Push:** a configured mobile or web app asset and a registered user or device identifier.
- **Live Chat or In-App Messaging:** a configured asset, app and user identifiers, and any required flow or webhook configuration.
- **Android or iOS SDK work:** the relevant SDK, platform credentials, and a test application or device.

For MCP-backed Production messaging, an organization administrator must enable the MCP server in Webex Control Hub and Webex Connect Tenant Settings. The tenant also needs an approved SMS phone number or supported Email asset with an approved AI Agent Messaging use case. Sandbox does not use the Production CPaaS MCP server.

Store secrets only in protected local configuration or the AI host's secure credential store. Do not put Service Keys, JWTs, MCP tokens, platform credentials, or tenant secrets in a prompt, skill package, plugin, public issue, or committed `.env` file.
