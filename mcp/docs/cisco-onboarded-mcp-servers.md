---
type: Guide
title: Cisco Onboarded MCP Servers | Overview
display_title: Overview
canonical_url: https://developer.webex.com/docs/cisco-onboarded-mcp-servers
content_type: documentation
product_group:
- webex-suite
- webex-contact-center
categories:
- mcp
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/cisco-onboarded-mcp-servers)

Cisco Onboarded Servers are developed by third-parties but onboarded by Cisco. We don't own these servers, and they are meant to be consumed by Webex AI clients. If you have any issues with the functionality of one of these servers, please reach out to the developer using the links below.

## Box

The Box MCP Server allows Webex users to manage content and collaborate securely within the chat interface.

- **Server URL:** `https://mcp.box.com`
- **Auth Type:** OAuth 2.0 Authorization Code
- **More details:** [Box MCP Server documentation](https://developer.box.com/guides/box-mcp/remote)

## Calendly

The Calendly MCP Server provides a secure integration layer built on the Model Context Protocol (MCP), enabling seamless scheduling and calendar management within Webex.

- **Server URL:** `https://mcp.calendly.com`
- **Auth Type:** OAuth 2.0 Authorization Code
- **More details:** [Calendly MCP Server documentation](https://developer.calendly.com/calendly-mcp-server)

## Figma

The Figma MCP Server acts as a secure bridge that allows AI development tools to read live design data — design tokens, components, and file structures — from Figma design files.

- **Server URL:** `https://mcp.figma.com/mcp`
- **Auth Type:** OAuth 2.0 Authorization Code
- **More details:** [Figma MCP Server guide](https://help.figma.com/hc/en-us/articles/32132100833559-Guide-to-the-Figma-MCP-server)

## GitHub

The GitHub MCP Server streamlines development by letting you manage repositories, track issues, and receive real-time notifications for pull requests and commits directly in Webex.

- **Server URL:** `https://api.githubcopilot.com/mcp`
- **Auth Type:** OAuth 2.0 Authorization Code
- **More details:** [GitHub MCP Server repository](https://github.com/github/github-mcp-server)

## Google Calendar

The Google Calendar MCP Server enables seamless integration between Google Calendar and Webex, allowing users to schedule and join meetings directly from their Google Workspace calendar.

- **Server URL:** `https://calendarmcp.googleapis.com/mcp/v1`
- **Auth Type:** OAuth 2.0 Authorization Code
- **More details:** [Google Calendar MCP Server documentation](https://developers.google.com/workspace/calendar/api/guides/configure-mcp-server)

## HubSpot

The HubSpot MCP Server provides a secure, scalable integration layer built on the Model Context Protocol (MCP), enabling seamless connectivity between HubSpot's marketing and sales platform and Webex.

- **Server URL:** `https://mcp.hubspot.com`
- **Auth Type:** OAuth 2.0 Authorization Code
- **More details:** [HubSpot MCP Server documentation](https://developers.hubspot.com/mcp)

## Jira

The Atlassian MCP Server allows Webex users to interact with Jira, Compass, and Confluence data in real time.

- **Server URL:** `https://mcp.atlassian.com/v1/mcp`
- **Auth Type:** OAuth 2.0 Authorization Code
- **More details:** [Atlassian Remote MCP Server documentation](https://support.atlassian.com/atlassian-rovo-mcp-server/docs/getting-started-with-the-atlassian-remote-mcp-server/)

## Miro

The Miro MCP Server is a service hosted by Miro that implements the Model Context Protocol (MCP), acting as a secure bridge between your AI development tools and live Miro boards.

- **Server URL:** `https://mcp.miro.com/`
- **Auth Type:** OAuth 2.0 Authorization Code
- **More details:** [Miro MCP Server documentation](https://developers.miro.com/docs/miro-mcp)

## PagerDuty

The PagerDuty MCP Server integrates PagerDuty's real-time incident management with Webex collaboration via Model Context Protocol (MCP).

- **Server URL:** `https://mcp.pagerduty.com/mcp`
- **Auth Type:** User Token
- **More details:** [PagerDuty MCP Server documentation](https://support.pagerduty.com/main/docs/pagerduty-mcp-server)

## Salesforce

Salesforce SObject All is a Salesforce-hosted MCP server that allows approved users to access standard and custom Salesforce objects from MCP-compatible AI experiences registered with Webex. It supports schema discovery, record querying, search, creation, updates, and deletion.

- **Server URL:** `https://api.salesforce.com/platform/mcp/v1/platform/sobject-all`
- **Auth Type:** OAuth 2.0 Authorization Code
- **More details:** [Salesforce Hosted MCP Servers Overview](https://developer.salesforce.com/docs/platform/hosted-mcp-servers/guide/hosted-mcp-servers-overview.html)
