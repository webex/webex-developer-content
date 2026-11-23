---
type: Excerpt
canonical_url: https://developer.webex.com/docs/buttons-and-cards
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Limitations
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/buttons-and-cards). [Full Markdown](../../../../docs/buttons-and-cards.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Give new levels of interactivity to Webex users by adding Buttons and Cards to your apps.

## Selected section

## Limitations

* Webex supports Adaptive Cards Version 1.3.
* The following card elements are not supported: `Media`.
* The following card properties are not supported: `fallback` for card elements, `fallbackText`, `requires`, and `speak`.
* The `height` property of the `ColumnSet` element is not supported.
* Cards may include up to twenty actions (using `ActionSet` gives you more freedom).
* Only one card can be sent per request.
* Editing of Cards on User interaction is possible only for cards with no images, pre or post Edit.
* Images in the SVG are not supported.
