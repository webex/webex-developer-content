---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-iframe-shell-migration
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Who Should Use This Guide
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/desktop-iframe-shell-migration). [Full Markdown](../../../../docs/desktop-iframe-shell-migration.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Developer guidance for validating custom Desktop widgets, mitigating overlay clipping, refactoring host DOM dependencies, and communicating between sibling widgets.

## Selected section

## Who Should Use This Guide

Use this guide if you build, configure, or maintain a Webex Contact Center Desktop custom widget that will run in the iframe shell.

This guide is especially relevant if your widget:

- Uses Momentum UI `md-*` components.
- Opens floating UI, such as dropdowns, menus, tooltips, popovers, dialogs, or custom panels.
- Is placed in a header slot, such as `area.advancedHeader[*]` or `area.header.*`.
- Reads or modifies Desktop host DOM or another widget's DOM.
- Sends or listens for events or data shared with another widget.
