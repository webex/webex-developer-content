---
type: Guide
title: Webex MCP Server | Vidcast MCP Server
display_title: Vidcast MCP Server
canonical_url: https://developer.webex.com/docs/vidcast-mcp-server
content_type: documentation
product_group:
- webex-suite
- webex-contact-center
categories:
- mcp
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/vidcast-mcp-server)

## What is Vidcast MCP Server?

Vidcast MCP Server is a Model Context Protocol (MCP) integration that enables AI assistants and agents to interact with the Vidcast video platform data. Vidcast is the Webex Suite's enterprise video solution. It exposes 29 tools that allow agents to search, browse, analyze, and retrieve information from Vidcast videos, playlists, pages, and user activity — all through a standardized MCP interface with OAuth-based authentication.

> **Prerequisites:** This MCP server must be enabled by your organization's admin in Webex Control Hub before it can be used. See [Provisioning on Control Hub](https://developer.webex.com/docs/provisioning-on-control-hub) for details.

- **Server URL:** `https://mcp.webexapis.com/mcp/vidcast`

## Tools

29 tools covering video discovery, content, engagement, analytics, recommendations, sharing, and notifications:

### Video Discovery & Search (4)

| Tool | Description |
|------|-------------|
| `vidcast-search-videos` | Search Vidcast videos by keywords (supports sorting and transcript inclusion) |
| `vidcast-search-pages` | Search Vidcast Pages by keywords |
| `vidcast-search-playlists` | Search Vidcast Playlists by keywords |
| `vidcast-search-users` | Search for Vidcast users by name or email |

### Video Library & Browsing (7)

| Tool | Description |
|------|-------------|
| `vidcast-list-my-videos` | List the authenticated user's video library (supports filtering by date, source, share type) |
| `vidcast-list-shared-with-me` | List videos shared with the authenticated user |
| `vidcast-list-recently-viewed-videos` | List recently viewed videos |
| `vidcast-list-pages` | List pages by kind (own/shared/collaborative/recent) |
| `vidcast-list-playlists` | List playlists by kind (own/shared/collaborative/recent) |
| `vidcast-get-shared-video` | Get a shared video by shareId |
| `vidcast-get-author-videos` | Get latest videos for an author by userId |

### Video Content & AI (2)

| Tool | Description |
|------|-------------|
| `vidcast-get-video-transcript` | Retrieve full transcript for a video |
| `vidcast-get-video-highlights` | Retrieve AI-generated highlights for a video |

### Engagement & Social (3)

| Tool | Description |
|------|-------------|
| `vidcast-get-video-comments` | List comments for a shared video |
| `vidcast-get-video-comment-replies` | List replies for a comment thread |
| `vidcast-get-video-reactions` | List emoji reactions for a shared video |

### Analytics & Insights (4)

| Tool | Description |
|------|-------------|
| `vidcast-get-video-insights` | Get analytics summary for a specific video |
| `vidcast-get-video-insights-views` | Get views timeseries for a video over a period |
| `vidcast-get-video-insights-retention` | Get retention analytics for a video |
| `vidcast-get-user-insights` | Get analytics summary for the authenticated user |
| `vidcast-get-user-insights-views` | Get views timeseries for the authenticated user |

### Recommendations (3)

| Tool | Description |
|------|-------------|
| `vidcast-recommend-watch-next` | Get watch-next recommendations using a reference item |
| `vidcast-recommend-top-videos` | Get top recommended videos for the user |
| `vidcast-recommend-trending-videos` | Get trending recommended videos for the user |

### Sharing & Access (3)

| Tool | Description |
|------|-------------|
| `vidcast-get-sharing-info` | Get sharing/access configuration for a resource |
| `vidcast-get-author-info` | Get author profile info by userId |
| `vidcast-list-access-requests` | List access requests for a shared resource |

### Notifications (2)

| Tool | Description |
|------|-------------|
| `vidcast-check-notifications` | Quick check if there are unread notifications (boolean) |
| `vidcast-list-notifications` | List user notifications (comments, reactions, access requests, shares) |

## Connect to your MCP Client

Select your AI client to get connection instructions:

- [Amazon Quick](https://developer.webex.com/docs/webex-agentic-mcp-servers-amazon-quick)
- [Claude Code](https://developer.webex.com/docs/webex-agentic-mcp-servers-claude-code)
- [Claude Desktop](https://developer.webex.com/docs/webex-agentic-mcp-servers-claude-desktop)
- [Codex](https://developer.webex.com/docs/webex-agentic-mcp-servers-codex)
- [Copilot Studio](https://developer.webex.com/docs/webex-agentic-mcp-servers-copilot-studio)
- [Cursor](https://developer.webex.com/docs/webex-agentic-mcp-servers-cursor)
- [Gemini CLI](https://developer.webex.com/docs/webex-agentic-mcp-servers-gemini-cli)
- [VS Code](https://developer.webex.com/docs/webex-agentic-mcp-servers-vscode)

## Authentication

**Auth Type:** OAuth 2.0 Bearer Token

**Issuer:** `https://webexapis.com`

**Flow:** The MCP client obtains a Webex OAuth token and passes it via the `Authorization: Bearer <token>` header. The server forwards it to each plugin, and plugins call the Webex REST API on behalf of the authenticated user.

**Rate limits:** 120 invocations per 60 seconds, max 10 concurrent requests

## Scopes

3 OAuth scopes required:

| Scope | Description |
|-------|-------------|
| `spark:mcp` | Required for MCP server connection |
| `Identity:Organization` | Access to organization-level identity information |
| `Identity:Config` | Access to identity configuration |

**Full scope string:**

```sh
spark:mcp Identity:Organization Identity:Config
```
