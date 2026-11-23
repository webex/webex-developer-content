---
type: Excerpt
canonical_url: https://developer.webex.com/docs/embedded-apps-reference
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Basic Usage
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/embedded-apps-reference). [Full Markdown](../../../../docs/embedded-apps-reference.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Selected section

## Basic Usage

To add the Embedded Apps Framework to your web application add the following to the `<HEAD>` of your app's main HTML page:

```html
<script src="https://binaries.webex.com/static-content-pipeline/webex-embedded-app/v1/webex-embedded-app-sdk.js" defer></script>
```

In your app's main index.js file create a new `Webex.Application` instance and create a function to handle the `onReady()` promise when it resolves successfully.

```javascript
var app = new window.Webex.Application();

app.onReady().then(function () {
  console.log('App is ready. App info:', app);
});
```
