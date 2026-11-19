---
type: Excerpt
canonical_url: https://developer.webex.com/docs/ea-tips-tricks-test
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Ensuring the Framework is Loaded and Ready
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/ea-tips-tricks-test). [Full Markdown](../../../../docs/ea-tips-tricks-test.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

---

**[Embedded Apps Guide](https://developer.webex.com/docs/ea-developer-guide-test) > Workflow**
* * * 

## Selected section

## Ensuring the Framework is Loaded and Ready

Once the embedded app framework is loaded and ready to use, it calls your app's `onReady` promise handler, for example:

```javascript
// Create Webex app object and initialize your application
var app = new window.Webex.Application();

app.onReady().then(() => {
    console.log("Framework is ready.");
}
```

However, if this code is parsed and executed before the framework's JavaScript library has finished loading, an 'undefined' runtime error will be generated since the `window.Webex` object doesn't yet exist. To avoid this you can either use the `defer` attribute on the `<script>` tag used to load the framework library, or modify your code to defer creation of the `app` object until `window.Webex` exists. Both of these approaches are described below.

* [Using the defer Script Tag Attribute](https://developer.webex.com/docs/embedded-apps-guide#defer-attribute)
* [Wait Until the Webex Object Exists](https://developer.webex.com/docs/embedded-apps-guide#waitforwebex)

<a id="defer-attribute"></a>
