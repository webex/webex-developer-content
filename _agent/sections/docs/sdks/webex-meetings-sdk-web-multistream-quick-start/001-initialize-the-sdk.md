---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-multistream-quick-start
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Initialize the SDK
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-multistream-quick-start). [Full Markdown](../../../../../docs/sdks/webex-meetings-sdk-web-multistream-quick-start.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Setup Remote Media Event Listeners](004-setup-remote-media-event-listeners.md)

## Article introduction

With multistream, developers gain greater flexibility when displaying remote media streams. Instead of receiving a single stream featuring all participants, multistream enables the showcasing of multiple streams simultaneously. This means you can easily view each remote participant's stream individually, enhancing clarity and engagement during collaborative sessions.

---

This guide provides a quick glimpse into consuming multistream in Webex Meetings using the Webex JavaScript SDK. You'll find code snippets below that can quickly get you up and running.

## Selected section

## Initialize the SDK

To work with the multistream feature you'll need to install via npm or yarn or reference via an HTML `<script>` tag, the Meetings Web SDK version 3.1.0 or higher:

### NPM

```bash
npm install webex
```

### Yarn

```bash
yarn add webex
```

### HTML

```html
<script defer src="https://unpkg.com/webex@3.7.0/umd/webex.min.js"></script>
```
