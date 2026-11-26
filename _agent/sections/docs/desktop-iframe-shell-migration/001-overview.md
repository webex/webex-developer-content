---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-iframe-shell-migration
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Overview
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/desktop-iframe-shell-migration). [Full Markdown](../../../../docs/desktop-iframe-shell-migration.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Developer guidance for validating custom Desktop widgets, mitigating overlay clipping, refactoring host DOM dependencies, and communicating between sibling widgets.

## Selected section

## Overview

This guide explains what changes in the new runtime model, which widget behaviors require validation or code changes, and how to update widgets that rely on overlays, host-page DOM access, or events shared with other widgets.

Webex Contact Center Desktop is moving custom widgets into an iframe shell. In the legacy model, a widget runs directly inside the Desktop page and shares the same document as the host application. In the iframe shell model, each widget runs in its own isolated iframe document—with its own DOM and its own browser storage (`localStorage`, `sessionStorage`, and cookies) separate from the host application.

This isolation improves stability and security, but it changes how widgets interact with shared page resources:

| Area | What changes | Required action |
| --- | --- | --- |
| Momentum UI `md-*` components | Momentum UI is made available inside the iframe shell. | No code change required. Confirm the widget renders correctly. |
| Floating overlays | Dropdowns, menus, tooltips, popovers, dialogs, and similar UI cannot render outside the iframe boundary. | Test all overlays. Increase the widget slot size when possible, or use the Desktop popover SDK for header widgets. |
| Host DOM access | A widget can no longer query or manipulate DOM elements owned by the host Desktop page or by sibling widgets. | Refactor the widget to use supported APIs and keep DOM access inside the widget's own subtree. |
| Host storage and cookies | A widget can no longer read or write the host Desktop application's `localStorage`, `sessionStorage`, or cookies (or another widget's storage). | Get host and agent data from the supported Desktop SDK instead of host storage. Keep storage within your own widget. |
| Sibling widget communication | Each widget has its own `window`. `CustomEvent`s, `window` events, and shared globals no longer reach other widgets. | Send data to sibling widgets with `postMessage`. Desktop relays the message between widget iframes. |



> **Working examples**
>
> The [Webex Contact Center widget starter](https://github.com/CiscoDevNet/webex-contact-center-widget-starter/tree/master/Examples/Widgets/iframe-shell) has small widgets that show each issue in this guide in its broken and fixed form, with source code. See [Try the Iframe Shell Examples](https://developer.webex.com/docs/desktop-iframe-shell-migration#try-the-iframe-shell-examples).
