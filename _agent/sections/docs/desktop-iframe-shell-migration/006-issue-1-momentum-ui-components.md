---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-iframe-shell-migration
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- 'Issue 1: Momentum UI Components'
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/desktop-iframe-shell-migration). [Full Markdown](../../../../docs/desktop-iframe-shell-migration.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Developer guidance for validating custom Desktop widgets, mitigating overlay clipping, refactoring host DOM dependencies, and communicating between sibling widgets.

## Selected section

## Issue 1: Momentum UI Components

### What Happens

Some widgets use Momentum UI web components such as:

- `md-button`
- `md-input`
- `md-combobox`
- `md-dropdown`
- `md-tooltip`
- `md-modal`

In the legacy model, these components may have worked because the Desktop host page already loaded Momentum UI. In the iframe shell model, the widget runs in a separate document, so shared globals from the host page are not automatically available.

### What the Iframe Shell Provides

The iframe shell loads Momentum UI inside the widget iframe. As a result, `md-*` custom elements are registered in the iframe document and can render normally.

### What You Need to Do

You do not need to bundle Momentum UI or rewrite Momentum component markup just to make `md-*` elements render.

You should still test any Momentum component that opens floating UI. Rendering and clipping are separate concerns:

- Inline components render inside the widget area and are not expected to clip.
- Overlay components can be clipped if their floating panel extends beyond the iframe boundary.

### Inline Components

Inline components are generally safe because they render inside their parent container:

- `md-button`
- `md-input`
- `md-label`
- `md-icon`
- `md-checkbox`
- `md-spinner`
- `md-tab`
- `md-avatar`
- `md-badge`
- `md-list`

### Overlay Components

Overlay components require validation because their floating content may extend beyond the iframe boundary:

- `md-tooltip`
- `md-menu-overlay`
- `md-popover`
- `md-combobox`
- `md-dropdown`
- `md-modal`
- `md-dialog`
- `md-datepicker`
- `md-coachmark`
- `md-floating-modal`
- `md-bottom-sheet`
