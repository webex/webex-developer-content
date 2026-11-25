---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-iframe-shell-migration
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Quick Guidance
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/desktop-iframe-shell-migration). [Full Markdown](../../../../docs/desktop-iframe-shell-migration.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Developer guidance for validating custom Desktop widgets, mitigating overlay clipping, refactoring host DOM dependencies, and communicating between sibling widgets.

## Selected section

## Quick Guidance

Most widgets do not require changes. The iframe shell provides Momentum UI, proxies the Desktop SDK, and relays supported events.

You may need to act if your widget does any of the following:

- Opens floating UI, such as dropdowns, menus, tooltips, comboboxes, date pickers, modals, dialogs, or custom absolute-positioned panels.
- Opens an overlay from a header slot, such as `area.advancedHeader[*]` or `area.header.*`.
- Reads or modifies DOM elements that the widget did not create, including host Desktop elements or elements inside another widget.
- Uses `CustomEvent`, `window` events, shared globals, or shared storage to pass data to another widget.

If your widget only uses inline controls, such as buttons, inputs, labels, icons, checkboxes, spinners, tabs, avatars, or badges, you generally only need to validate that the widget renders correctly in the iframe shell. If the widget is in a header slot, also confirm its width. See Header widget width in [Impact Categories](https://developer.webex.com/docs/desktop-iframe-shell-migration#impact-categories).
