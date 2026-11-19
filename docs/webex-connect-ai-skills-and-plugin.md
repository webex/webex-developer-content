---
type: Guide
title: Webex Connect AI Skills and Plugin
display_title: Webex Connect AI Skills and Plugin
canonical_url: https://developer.webex.com/docs/webex-connect-ai-skills-and-plugin
content_type: documentation
product_group:
- webex-connect
categories:
- mcp
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/webex-connect-ai-skills-and-plugin)

Install and use Webex Connect AI Skills with Codex, Claude Code, Cursor, or standalone skill packages. This guide explains the 19 available skills, plugin and skill installation, tenant and credential prerequisites, common workflows, MCP setup, and production safeguards.

## Overview

Webex Connect skills are focused instruction packages that help an AI coding agent build, configure, and operate Webex Connect workflows. They explain when a workflow applies, what information it needs, how to validate the request, and how to handle the result.

The public Webex Skills repository provides two ways to install these instructions:

- **Standalone skills** install selected workflows individually.
- **Webex Connect AI plugin** bundles the Connect skills with host-specific commands, rules, manifests, and branding.

The plugin includes 19 independently packaged skills. The source repository currently identifies the plugin as a beta release. The skill set and versions can change; the table below reflects the current catalog.

Installing a skill or plugin does not create a Webex Connect tenant, register a mobile device, approve a sender, configure credentials, or enable an MCP connection. Complete the relevant setup steps in this guide before using API-backed workflows.

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

## Complete the task

### Choose an installation

Choose standalone skills when you need a smaller, auditable set of workflows. Choose the plugin when you want the bundled Webex Connect workflows, commands, and rules together.

The plugin supports Codex, Claude Code, and Cursor. A standalone skill can support additional clients through its installer. See the [Webex Skills repository](https://github.com/webex/webex-skills) for the current package source and release information.

### Skill catalog

Use the message router for an outbound send request. It selects one channel-specific skill and adds setup, Contact Policy, webhook, or Sandbox guidance when the task requires it.

| Skill | What it does |
| --- | --- |
| [`webex-connect-setup`](https://github.com/webex/webex-skills/blob/main/skills/webex-connect-setup/skill/webex-connect-setup/SKILL.md) | Selects Sandbox or Production, confirms tenant region and API hosts, prepares local configuration, collects required credentials, and configures the supported Production SMS or Email MCP endpoint. SDK and widget builders do not require this API setup. |
| [`webexconnect-android-push-inapp-messaging-builder`](https://github.com/webex/webex-skills/blob/main/skills/webexconnect-android-push-inapp-messaging-builder/skill/webexconnect-android-push-inapp-messaging-builder/SKILL.md) | Builds or repairs native Android applications using Webex Connect Push Notifications or In-App Messaging, including registration, chat, notifications, and QA. |
| [`webexconnect-apple-messages-for-business-sendmessage`](https://github.com/webex/webex-skills/blob/main/skills/webexconnect-apple-messages-for-business-sendmessage/skill/webexconnect-apple-messages-for-business-sendmessage/SKILL.md) | Builds and validates Apple Messages for Business API v1 text and rich messages, attachments, callbacks, and delivery handling. |
| [`webexconnect-contact-policy`](https://github.com/webex/webex-skills/blob/main/skills/webexconnect-contact-policy/skill/webexconnect-contact-policy/SKILL.md) | Uses Contact Policy APIs to manage consent, opt-in and opt-out, channel checks, frequency caps, and send-policy enforcement. |
| [`webexconnect-digital-asset-creation`](https://github.com/webex/webex-skills/blob/main/skills/webexconnect-digital-asset-creation/skill/webexconnect-digital-asset-creation/SKILL.md) | Creates, retrieves, and updates Chat, Email, Facebook Messenger, or WhatsApp assets using the selected operation schema and tenant region. |
| [`webexconnect-email-sendmessage`](https://github.com/webex/webex-skills/blob/main/skills/webexconnect-email-sendmessage/skill/webexconnect-email-sendmessage/SKILL.md) | Builds, validates, or sends Email with Send Message API v2 or configured Email MCP, including sender discovery, content, callbacks, and receipts. |
| [`webexconnect-facebook-messenger-sendmessage`](https://github.com/webex/webex-skills/blob/main/skills/webexconnect-facebook-messenger-sendmessage/skill/webexconnect-facebook-messenger-sendmessage/SKILL.md) | Builds and validates Facebook Messenger API v1 messages for Page-scoped recipients, text, attachments, interactive replies, and callbacks. |
| [`webexconnect-ios-push-inapp-messaging-builder`](https://github.com/webex/webex-skills/blob/main/skills/webexconnect-ios-push-inapp-messaging-builder/skill/webexconnect-ios-push-inapp-messaging-builder/SKILL.md) | Builds or repairs native iOS applications using Webex Connect Push Notifications or In-App Messaging, including registration, chat, notifications, and QA. |
| [`webexconnect-livechat-inapp-sendmessage`](https://github.com/webex/webex-skills/blob/main/skills/webexconnect-livechat-inapp-sendmessage/skill/webexconnect-livechat-inapp-sendmessage/SKILL.md) | Builds and validates Live Chat and In-App Messaging API v1 requests for messages, threads, attachments, quick replies, notifications, and callbacks. |
| [`webexconnect-livechat-widget`](https://github.com/webex/webex-skills/blob/main/skills/webexconnect-livechat-widget/skill/webexconnect-livechat-widget/SKILL.md) | Builds or troubleshoots browser Live Chat widgets using the Webex Connect JavaScript SDK, including registration, threads, messaging, and events. |
| [`webexconnect-mms-sendmessage`](https://github.com/webex/webex-skills/blob/main/skills/webexconnect-mms-sendmessage/skill/webexconnect-mms-sendmessage/SKILL.md) | Builds and validates Send Message API v2 MMS requests with media, fallback text, receipts, and callbacks. |
| [`webexconnect-push-sendmessage`](https://github.com/webex/webex-skills/blob/main/skills/webexconnect-push-sendmessage/skill/webexconnect-push-sendmessage/SKILL.md) | Builds and validates Push Messaging API v1 requests for registered users or devices, platform payloads, notifications, and callbacks. |
| [`webexconnect-rcs-sendmessage`](https://github.com/webex/webex-skills/blob/main/skills/webexconnect-rcs-sendmessage/skill/webexconnect-rcs-sendmessage/SKILL.md) | Builds and validates Send Message API v2 RCS requests, including capability checks, rich content, templates, and SMS fallback. |
| [`webexconnect-sandbox`](https://github.com/webex/webex-skills/blob/main/skills/webexconnect-sandbox/skill/webexconnect-sandbox/SKILL.md) | Plans supported Sandbox SMS, Voice, and WhatsApp API tests with verified recipients and Sandbox-specific limits. It does not configure Production MCP. |
| [`webexconnect-sendmessage`](https://github.com/webex/webex-skills/blob/main/skills/webexconnect-sendmessage/skill/webexconnect-sendmessage/SKILL.md) | Routes an outbound request to the right channel skill and adds shared setup, Contact Policy, webhook, or Sandbox guidance when needed. |
| [`webexconnect-sms-sendmessage`](https://github.com/webex/webex-skills/blob/main/skills/webexconnect-sms-sendmessage/skill/webexconnect-sms-sendmessage/SKILL.md) | Builds, validates, or sends SMS with Send Message API v2 or configured SMS MCP, including sender discovery, recipients, scheduling, receipts, and callbacks. |
| [`webexconnect-voice-sendmessage`](https://github.com/webex/webex-skills/blob/main/skills/webexconnect-voice-sendmessage/skill/webexconnect-voice-sendmessage/SKILL.md) | Builds and validates Voice API v1 and documented Send Message API v2 voice requests for outbound calls, text-to-speech, media, callbacks, and call status. |
| [`webexconnect-webhooks-events`](https://github.com/webex/webex-skills/blob/main/skills/webexconnect-webhooks-events/skill/webexconnect-webhooks-events/SKILL.md) | Builds and troubleshoots webhook receivers, callback verification, inbound events, Event API requests, retries, and data streams. |
| [`webexconnect-whatsapp-sendmessage`](https://github.com/webex/webex-skills/blob/main/skills/webexconnect-whatsapp-sendmessage/skill/webexconnect-whatsapp-sendmessage/SKILL.md) | Builds and validates WhatsApp API v1 session replies, approved templates, media, interactive content, and callbacks. |

### Install the bundled plugin

Clone the public repository once. Use a directory where you keep development tools, not your application project root:

```bash
git clone https://github.com/webex/webex-skills.git
cd webex-skills
```

The assembled, installable plugin is in `plugin-packages/webex-connect-ai/`. No local build step is required for normal installation.

#### Codex

Add the Webex Skills marketplace to Codex:

```bash
codex plugin marketplace add https://github.com/webex/webex-skills.git \
  --sparse .agents/plugins \
  --sparse plugin-packages/webex-connect-ai
```

Open Codex and run:

```text
/plugins
```

Select **Webex Skills**, choose **Webex Connect AI**, and select **Install plugin**. Complete any prompts, then start a new Codex session and confirm that the plugin appears in the plugin browser.

#### Claude Code

In a Claude Code session, add the public marketplace and install the plugin:

```text
/plugin marketplace add webex/webex-skills
/plugin install webex-connect-ai@webex-skills
```

Review the plugin details and select user, project, or local scope when prompted. Start a new Claude Code session after installation. Use `/plugin` to inspect installed and available plugins.

#### Cursor

Copy the assembled plugin into Cursor's local plugin directory:

```bash
mkdir -p ~/.cursor/plugins/local/webex-connect-ai
rsync -a --delete ./plugin-packages/webex-connect-ai/ ~/.cursor/plugins/local/webex-connect-ai/
```

Reload Cursor, open **Customize**, and confirm that the skills, commands, and rules are visible. Enterprise administrators may need to allow local plugin imports or distribute the plugin through a team marketplace.

### Install standalone skills

Choose a skill from the catalog and install its package. The packages are distributed as GitHub archives; they do not need to be published to the npm registry. Installers use `npx`.

For example, install the SMS skill for Codex at user scope:

```bash
npx --yes \
  --package https://raw.githubusercontent.com/webex/webex-skills/main/skills/webexconnect-sms-sendmessage/release/webexconnect-sms-sendmessage-latest.tgz \
  webexconnect-sms-sendmessage install --client codex --scope user
```

Install the setup skill as well when you plan to use API-backed workflows:

```bash
npx --yes \
  --package https://raw.githubusercontent.com/webex/webex-skills/main/skills/webex-connect-setup/release/webex-connect-setup-latest.tgz \
  webex-connect-setup install --client codex --scope user
```

Use `--scope project` to install into the current application project. Installer-supported clients include Codex, Claude Code, and GitHub Copilot; `--client all` installs for Codex, GitHub Copilot, and Claude Code. Check the selected skill's package metadata for the supported clients.

### Update an installation

Before updating, close active sessions using Webex Connect AI. After updating, restart or reload the host so it does not keep an older copy in memory. Updating a plugin or skill does not change the tenant, digital assets, sender IDs, project `.env`, or secure MCP credentials.

For a Codex Git-backed marketplace, refresh the source:

```bash
codex plugin marketplace upgrade webex-skills
```

Open `/plugins` in Codex to inspect Webex Connect AI and use the available plugin update action. If no update is offered, remove and reinstall the plugin from the refreshed **Webex Skills** marketplace. Start a new Codex session after updating.

For Claude Code, update the marketplace and plugin:

```text
/plugin marketplace update webex-skills
```

Or use the CLI:

```bash
claude plugin marketplace update webex-skills
claude plugin update webex-connect-ai@webex-skills
claude plugin list
```

For the local Cursor installation, update the `webex-skills` clone used during installation and copy the refreshed plugin files into Cursor's local plugin directory:

```bash
git pull --ff-only
rsync -a --delete ./plugin-packages/webex-connect-ai/ ~/.cursor/plugins/local/webex-connect-ai/
```

The trailing slashes copy the package contents, and `--delete` removes local files that are no longer in the source. Reload Cursor and confirm the updated skills, commands, and rules are visible.

To update a standalone skill, rerun its installer with the same client and scope and add `--force`. For example:

```bash
npx --yes \
  --package https://raw.githubusercontent.com/webex/webex-skills/main/skills/webexconnect-sms-sendmessage/release/webexconnect-sms-sendmessage-latest.tgz \
  webexconnect-sms-sendmessage install --client codex --scope user --force
```

Review local modifications before replacing a skill. For project installs, run from the target project and keep `--scope project`. Do not mix skill directories from different releases.

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

### MCP endpoints, region, and authentication

Use the Integration endpoint for the tenant's staging or preproduction environment, or the Production endpoint for its confirmed region. Do not guess an endpoint that is not listed.

| Webex Connect region | Production MCP server URL |
| --- | --- |
| ca (AWS Canada) | [https://mcp.ca.webexconnect.io/mcp/cpaas](https://mcp.ca.webexconnect.io/mcp/cpaas) |
| eu (AWS Ireland) | [https://mcp.eu.webexconnect.io/mcp/cpaas](https://mcp.eu.webexconnect.io/mcp/cpaas) |
| uk (AWS London) | [https://mcp.uk.webexconnect.io/mcp/cpaas](https://mcp.uk.webexconnect.io/mcp/cpaas) |
| us (United States) | [https://mcp.us.webexconnect.io/mcp/cpaas](https://mcp.us.webexconnect.io/mcp/cpaas) |
| in (AWS Mumbai) | [https://mcp.in.webexconnect.io/mcp/cpaas](https://mcp.in.webexconnect.io/mcp/cpaas) |
| au (AWS Sydney) | [https://mcp.au.webexconnect.io/mcp/cpaas](https://mcp.au.webexconnect.io/mcp/cpaas) |
| sg (AWS Singapore) | [https://mcp.sg.webexconnect.io/mcp/cpaas](https://mcp.sg.webexconnect.io/mcp/cpaas) |

The MCP server must be enabled by an organization administrator in Webex Control Hub and Webex Connect Tenant Settings. An approved SMS phone number or supported Email asset and an approved AI Agent Messaging use case are also required.

Codex supports token-based authentication with a Webex Client Integration Token (WCIT) that has the `spark:mcp` scope. Store the token as a bearer token in Codex's MCP server configuration; protect the local configuration file. The server requests any additional tool scopes at runtime through MCP elicitation. Cursor supports the same WCIT flow and also OAuth through an Integration App; register Cursor's fixed redirect URI `cursor://anysphere.cursor-mcp/oauth/callback`. Claude Code uses client-based browser OAuth; prepare the Integration App client ID, client secret, and matching callback URI listed above. Keep bearer tokens and client secrets in protected local configuration, never in a prompt or committed file.

- **Codex:** configure the selected URL and WCIT as the Authorization bearer token in Codex's MCP server configuration, then protect the local configuration file.
- **Claude Code:** add the selected URL with `claude mcp add --transport http` using the Integration App client ID, client secret, and registered callback port. Then run `/mcp`, select the server, and choose **Authenticate** to complete browser authorization. See the [Claude Code MCP setup guide](https://developer.webex.com/docs/webex-agentic-mcp-servers-claude-code) for the command and callback details.
- **Cursor:** use the one-click WCIT token flow or configure OAuth through the Integration App flow described in Cursor's MCP guide.

The CPaaS MCP server exposes sender discovery and non-templated SMS and Email messaging. Its tools are `webex-sender-ids`, `webex-sms-message`, and `webex-email-message`. Do not use Production MCP credentials for Sandbox. If your tenant region is not listed, confirm it with your administrator and use documented direct APIs until a supported MCP endpoint is confirmed.

Direct API credentials and MCP credentials are separate and are not interchangeable. Keep the selected tenant and environment in your local setup record without storing credential values there.

### Common use cases

| Use case | Skills to start with | Example |
| --- | --- | --- |
| Transactional or marketing messages | `webexconnect-sendmessage`, a channel-specific send skill, and `webexconnect-contact-policy` when consent rules apply | Send an approved order update, reminder, or campaign using the right channel and sender. |
| Digital-channel onboarding | `webexconnect-digital-asset-creation` | Create, retrieve, or update a Chat, Email, Facebook Messenger, or WhatsApp asset. |
| Customer support and live engagement | `webexconnect-livechat-widget` or `webexconnect-livechat-inapp-sendmessage` | Build a browser widget or support threaded Live Chat and In-App conversations. |
| Mobile engagement | Android or iOS Push and In-App Messaging builder; `webexconnect-push-sendmessage` | Build a mobile sample or send to a registered user or device. |
| Delivery operations | `webexconnect-webhooks-events` and the relevant channel skill | Process inbound events, delivery receipts, failures, callbacks, and retries. |
| Prototyping | `webexconnect-sandbox` | Test supported SMS, Voice, or WhatsApp flows with verified recipients and Sandbox limits. |

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

## Verify the result

- Confirm the installed plugin or skill and release in the AI host, then reload or restart the host.
- Ask the agent to list the Webex Connect skills and confirm that the expected workflows are available.
- For API-backed work, run setup as a preflight check and confirm the selected tenant, environment, region, endpoint, and required local credentials.
- For MCP, verify the intended regional URL, secure authentication, and the available sender discovery or messaging tools.
- Start with a test tenant, test asset, or test recipient when possible. Record message IDs, correlation IDs, request timestamps, and acceptance status.
- Treat an accepted or queued response as platform acceptance. Check receipts, callbacks, and tenant logs separately to confirm delivery.

## Security and operational guidance

- Review the plugin source and manifest before installing, especially from a third-party marketplace.
- Grant filesystem and MCP permissions only to workflows that need them.
- Keep secrets in an ignored local `.env` with owner-only access or in the host's secure credential store. Never paste bearer tokens or Service Keys into a public prompt, README, issue, generated source, or committed environment file.
- Use test recipients and assets before Production sends.
- Confirm the environment, tenant, sender, recipient, and payload before each irreversible action.
- Configure Contact Policy and opt-out handling for promotional messages.
- Treat API acceptance, provider delivery, and end-user display as separate states.

## Troubleshooting

### A skill is not discovered

Confirm that the selected skill is installed in the correct host or project skills directory, that its folder contains `SKILL.md`, and that the directory uses the expected skill name. Reload or restart the AI tool.

### The plugin is installed but its commands are missing

Check that the installed plugin package contains its manifests, `skills/`, `commands/`, and `rules/` directories. For local installs, confirm the plugin path points to `plugin-packages/webex-connect-ai/`, then reload the host.

### Sandbox setup asks for MCP authentication

Stop and confirm the selected environment. Sandbox does not use the Production CPaaS MCP server or its credentials.

### Sender discovery returns no compatible sender

Do not invent a sender ID. Ask the tenant administrator to approve or expose a sender for the intended channel and use case, then repeat discovery.

### A message is queued but not received

Queued means accepted for processing, not delivered. Check the recipient or device registration, sender configuration, channel credentials, provider status, webhook receipts, and tenant logs.

## Related resources

- [Webex Skills repository](https://github.com/webex/webex-skills)
- [Webex Connect skill and plugin catalog](https://github.com/webex/webex-skills/blob/main/PLUGINS.md)
- [Webex Connect plugin source](https://github.com/webex/webex-skills/tree/main/plugins/webex-connect-ai)
- [Webex Connect API overview](https://developers.webexconnect.io/reference/apioverview)
- [Webex Connect API authentication](https://developers.webexconnect.io/reference/api-authentication)
- [Webex Connect regional API endpoints](https://developers.webexconnect.io/reference/know-your-api-endpoints)
