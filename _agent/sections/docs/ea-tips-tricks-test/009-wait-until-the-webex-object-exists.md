---
type: Excerpt
canonical_url: https://developer.webex.com/docs/ea-tips-tricks-test
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Wait Until the Webex Object Exists
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/ea-tips-tricks-test). [Full Markdown](../../../../docs/ea-tips-tricks-test.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

---

**[Embedded Apps Guide](https://developer.webex.com/docs/ea-developer-guide-test) > Workflow**
* * * 

## Selected section

## Wait Until the Webex Object Exists

As an alternative to use the `defer` script tag attribute, your app code can defer creation of the main Webex app object until `window.Webex` exists. The framework will then automatically call your `onReady()` promise handler. For example, the following uses the `setInterval()` function before creating the `app` object.

```javascript
// Declare app object:
var app;

// Wait for window.Webex
var checkForWebex = setInterval(function() {
   if (window.Webex) {
      app = new window.Webex.Application();    
   }
}, 100); // check every 100ms

// Define onReady handler:
app.onReady().then(() => {
    console.log("Framework is ready.");
}
```
