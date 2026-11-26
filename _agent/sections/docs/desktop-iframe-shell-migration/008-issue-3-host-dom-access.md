---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-iframe-shell-migration
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- 'Issue 3: Host DOM Access'
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/desktop-iframe-shell-migration). [Full Markdown](../../../../docs/desktop-iframe-shell-migration.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Developer guidance for validating custom Desktop widgets, mitigating overlay clipping, refactoring host DOM dependencies, and communicating between sibling widgets.

## Selected section

## Issue 3: Host DOM Access

### What Happens

In the legacy model, a widget could sometimes access the host Desktop DOM because it shared the same document. For example, a widget might:

- Call `document.querySelector("agentx-app")`.
- Traverse a host element's `shadowRoot`.
- Attach listeners to host controls.
- Read or modify another widget's DOM.

In the iframe shell model, the widget can only access its own iframe document. Host elements and sibling widget elements are outside the iframe boundary.

### Required Action

Refactor the widget so it does not depend on DOM elements it did not create.

There is no supported host DOM shim or stand-in element for the Desktop page. Treat the widget iframe as the only DOM the widget is allowed to query or mutate.

### Refactoring Guidance

Use these rules when updating the widget:

- Remove selectors that target host Desktop elements or sibling widgets.
- Do not walk into another component's `shadowRoot`.
- Get agent and Desktop state from the supported Desktop SDK instead of scraping the host UI.
- Subscribe to supported SDK events instead of intercepting clicks on host controls.
- Keep DOM queries scoped to elements rendered by the widget.
- Degrade gracefully if optional data is not available.
- Use `postMessage` for supported communication between sibling widget iframes instead of reading another widget's DOM. See [Issue 4: Sibling Widget Communication](https://developer.webex.com/docs/desktop-iframe-shell-migration#issue-4-sibling-widget-communication).

**Rule of thumb:** if the widget touches an element it did not create, that code needs an iframe-safe refactor.



> **Example**
>
> [`sdk-init-widget`](https://github.com/CiscoDevNet/webex-contact-center-widget-starter/blob/master/Examples/Widgets/iframe-shell/src/sdk-init-widget.ts) starts with `Desktop.config.init()` and reads agent data from the SDK instead of calling `document.querySelector("agentx-app")`.
