---
type: Excerpt
canonical_url: https://developer.webex.com/docs/ea-tips-tricks-test
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Using the defer Script Tag Attribute
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/ea-tips-tricks-test). [Full Markdown](../../../../docs/ea-tips-tricks-test.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

---

**[Embedded Apps Guide](https://developer.webex.com/docs/ea-developer-guide-test) > Workflow**
* * * 

## Selected section

## Using the defer Script Tag Attribute

When present on a `<script>` tag, the `defer` attribute indicates to the embedded web view in which your app is running that the script should be executed after the document has been parsed. Scripts with the `defer` attribute execute in the order in which they appear in the document. For this reason the `<script>` tag that loads the embedded app framework must be declared before any `<script>` tag that loads your application code, as shown below.

```html
<head>
    <!-- Load the embedded app framework -->
    <script src="https://binaries.webex.com/static-content-pipeline/webex-embedded-app/v1/webex-embedded-app-sdk.js" defer></script>
    <!-- Load your app's main javascript file -->
    <script src="./index.js" defer></script>
</head>
```

With this setup your app's code is guaranteed to execute only after the framework is loaded. Without the `defer` attribute there's a chance that the `window.Webex` object will be `undefined` when your app's code attempts to use it. 

<a id="waitforwebex"></a>
