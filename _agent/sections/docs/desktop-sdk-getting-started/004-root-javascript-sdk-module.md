---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-sdk-getting-started
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Root JavaScript SDK Module
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/desktop-sdk-getting-started). [Full Markdown](../../../../docs/desktop-sdk-getting-started.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Install and initialize the Desktop SDK to access Desktop modules from custom widgets.

## Selected section

## Root JavaScript SDK Module

`Desktop` is the root module of the JavaScript SDK. The root module provides a reference to the following sub-modules:

- Configuration Module
- Localization Module
- Actions Module
- Logger Module
- Agent State Information Module
- Agent Contact Module
- Dialer Module
- Screen Pop Module
- Shortcut Key Module
- Call Monitoring Module
- Webex Metrics Module
- Schedule Callback Module
- Popover Module

**Example**

```javascript
import { Desktop } from "@wxcc-desktop/sdk";

const {
  config,
  i18n,
  actions,
  agentContact,
  agentStateInfo,
  dialer,
  logger,
  screenpop,
  shortcutKey, 
  webexMetricsInternal,
  scheduleCallback,
  popover,
} = Desktop;
```
