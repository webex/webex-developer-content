---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-iframe-shell-migration
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Widgets With Multiple Issues
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/desktop-iframe-shell-migration). [Full Markdown](../../../../docs/desktop-iframe-shell-migration.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Developer guidance for validating custom Desktop widgets, mitigating overlay clipping, refactoring host DOM dependencies, and communicating between sibling widgets.

## Selected section

## Widgets With Multiple Issues

Some widgets may be affected by more than one iframe shell behavior. Use this order of operations:

- If the widget opens an overlay from a header slot, address the header overlay issue first. Momentum UI rendering and slot sizing alone will not prevent header overlay clipping.
- If the widget also accesses host or sibling DOM, complete the host DOM refactor before go-live.
- If the widget passes data to other widgets, move that communication to `postMessage` before go-live.
- After code or layout changes, run the full testing checklist against the final iframe shell configuration.
