---
type: Excerpt
canonical_url: https://developer.webex.com/docs/vidcast-mcp-server
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Tools
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/vidcast-mcp-server). [Full Markdown](../../../../docs/vidcast-mcp-server.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Authentication](004-authentication.md) [Scopes](005-scopes.md)

## Selected section

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
