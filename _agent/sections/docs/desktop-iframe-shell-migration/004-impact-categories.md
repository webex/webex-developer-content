---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-iframe-shell-migration
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Impact Categories
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/desktop-iframe-shell-migration). [Full Markdown](../../../../docs/desktop-iframe-shell-migration.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Developer guidance for validating custom Desktop widgets, mitigating overlay clipping, refactoring host DOM dependencies, and communicating between sibling widgets.

## Selected section

## Impact Categories

| Category | Applies when | Primary action | Example |
| --- | --- | --- | --- |
| Momentum UI components | The widget uses Momentum UI `md-*` components that previously relied on the host page. | Confirm rendering. Test overlays if the widget uses overlay-prone components. | — |
| Header overlay risk | The widget opens floating UI from a header or `advancedHeader` slot. | Use the Desktop popover SDK or move the widget to a roomier slot. | [`header-clip-widget`](https://github.com/CiscoDevNet/webex-contact-center-widget-starter/blob/master/Examples/Widgets/iframe-shell/src/header-clip-widget.ts), [`header-popover-widget`](https://github.com/CiscoDevNet/webex-contact-center-widget-starter/blob/master/Examples/Widgets/iframe-shell/src/header-popover-widget.ts) |
| Header widget width | The widget renders in a header or `advancedHeader` slot. | Size the widget from its content, such as `display: inline-flex; width: max-content`. Do not use `width: 100%`. Confirm the widget is neither truncated nor wider than its content. | [`header-fit-widget`](https://github.com/CiscoDevNet/webex-contact-center-widget-starter/blob/master/Examples/Widgets/iframe-shell/src/header-fit-widget.ts), [`header-overflow-widget`](https://github.com/CiscoDevNet/webex-contact-center-widget-starter/blob/master/Examples/Widgets/iframe-shell/src/header-overflow-widget.ts) |
| Host DOM access | The widget queries or manipulates host Desktop DOM or another widget's DOM. | Refactor the widget to stop depending on DOM it did not create. | [`sdk-init-widget`](https://github.com/CiscoDevNet/webex-contact-center-widget-starter/blob/master/Examples/Widgets/iframe-shell/src/sdk-init-widget.ts) |
| Sibling widget communication | The widget sends data to, or receives data from, another widget. | Replace `CustomEvent`s and shared globals with `postMessage`. | [`sibling-bus-publisher`](https://github.com/CiscoDevNet/webex-contact-center-widget-starter/blob/master/Examples/Widgets/iframe-shell/src/sibling-bus-publisher.ts), [`sibling-bus-consumer`](https://github.com/CiscoDevNet/webex-contact-center-widget-starter/blob/master/Examples/Widgets/iframe-shell/src/sibling-bus-consumer.ts) |
