---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-iframe-shell-migration
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Testing Checklist
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/desktop-iframe-shell-migration). [Full Markdown](../../../../docs/desktop-iframe-shell-migration.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Developer guidance for validating custom Desktop widgets, mitigating overlay clipping, refactoring host DOM dependencies, and communicating between sibling widgets.

## Selected section

## Testing Checklist

Run this checklist after enabling the widget in the iframe shell.

1. Note the widget script URL, layout slot, and whether it uses Momentum UI components, floating overlays, host DOM access, or sibling widget communication.
2. To see expected iframe shell behavior first, run the sample layout in [Try the Iframe Shell Examples](https://developer.webex.com/docs/desktop-iframe-shell-migration#try-the-iframe-shell-examples). Load your widget from an absolute `script` URL.
3. Confirm that the widget renders correctly.
4. Confirm that buttons, inputs, icons, labels, and other inline controls are styled correctly.
5. Open every overlay the widget can produce.
6. Validate each dropdown, menu, combobox, tooltip, date picker, modal, dialog, drawer, and popover.
7. Confirm that no overlay is clipped at the iframe edge.
8. If the widget is in `advancedHeader` or another header slot, use the header mitigation path. Do not rely on CSS overflow or slot sizing.
9. If the widget is in a header slot, confirm that it sizes from its content rather than `width: 100%`, and that it is neither truncated nor wider than its content.
10. Test with production-realistic Desktop window sizes, including smaller windows.
11. Search the widget code for host DOM or sibling widget DOM access.
12. Refactor any DOM access that targets elements the widget did not create.
13. Confirm that every message sent to a sibling widget arrives, and that no `CustomEvent`, global, or shared storage is still used to reach another widget.
14. If multiple deployments use the same script URL, layout slot, and layout `attributes` and `properties`, validate the shared bundle once and apply that result to each matching deployment.
