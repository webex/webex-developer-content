---
type: Excerpt
canonical_url: https://developer.webex.com/docs/embedded-apps-api-reference
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Basic Usage
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/embedded-apps-api-reference). [Full Markdown](../../../../docs/embedded-apps-api-reference.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This is the complete API reference for the Webex Embedded Apps 1.x Framework.

---



> **Warning**
>
> The Embedded Apps version 1 SDK has been deprecated and will be supported based upon the following [support policy](https://developer.webex.com/docs/webex-api-and-sdk-support-policy#current-end-of-life-eol-notices). For new customers accessing this page, please see the [Embedded Apps version 2 SDK API Reference](https://eaf-sdk.webex.com/). For existing version 1 SDK customers, please see [Migration from 1.x to 2.x](https://eaf-sdk.webex.com/#migration-from-1x-to-2x). New features will only be added to the version 2 SDK.

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
