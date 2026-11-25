---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-iframe-shell-migration
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Try the Iframe Shell Examples
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/desktop-iframe-shell-migration). [Full Markdown](../../../../docs/desktop-iframe-shell-migration.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Developer guidance for validating custom Desktop widgets, mitigating overlay clipping, refactoring host DOM dependencies, and communicating between sibling widgets.

## Selected section

## Try the Iframe Shell Examples

The Webex Contact Center widget starter includes small widgets that show each iframe shell issue in its broken and fixed form. Run them in Desktop once so you know what correct behavior looks like, then compare with your own widget.

| Widget | Slot | Shows |
| --- | --- | --- |
| `header-clip-widget` | `advancedHeader` | `md-menu-overlay` opened from the header and clipped by the iframe (broken). |
| `header-popover-widget` | `advancedHeader` | The same panel opened with `Desktop.popover` and rendered outside the iframe (fixed). |
| `sibling-bus-publisher` | `advancedHeader` | **CE** sends a `CustomEvent` that stays in its own iframe (broken). **PM** sends a `postMessage` that Desktop relays (fixed). |
| `sibling-bus-consumer` | `navigation` | Receives only the relayed `postMessage`. |
| `sdk-init-widget` | `navigation` | Starts with `Desktop.config.init()` instead of querying `agentx-app`. |

Source for each widget: [Examples/Widgets/iframe-shell/src](https://github.com/CiscoDevNet/webex-contact-center-widget-starter/tree/master/Examples/Widgets/iframe-shell/src).

**Before you begin**

Understand the JSON layout format. For more information on JSON layout, see [Create custom desktop layout](https://help.webex.com/en-us/article/ng08gqeb/Create-custom-desktop-layout) in Webex Help Center.

**Procedure**

1. Download the sample layout [Iframe_Shell_Partner_Fixes.json](https://github.com/CiscoDevNet/webex-contact-center-widget-starter/blob/master/Examples/Layouts/Iframe_Shell_Partner_Fixes.json).
2. Upload the layout to a test team in the Webex Contact Center Management Portal, and sign in to Desktop as an agent on that team.
3. In the header, open the menu in `header-clip-widget` and confirm that it is clipped. Open `header-popover-widget` and confirm that the panel renders below the header.
4. Open the **Iframe shell fixes** navigation page. In the header, click **CE** and then **PM** on `sibling-bus-publisher`. Confirm that `sibling-bus-consumer` shows only the **PM** message.
5. To test your own widget the same way, replace one `comp` and `script` pair with your widget. Use an absolute `script` URL so that Desktop loads the widget in the iframe shell.

```json
{
    "comp": "vendor-widget",
    "script": "https://widget.example.com/widgets/vendor.js"
}
```



> **Info**
>
> Storybook, a local dev server, and other in-page previews do not run the iframe shell. They do not show overlay clipping, `Desktop.popover`, or sibling relay. Validate in Desktop.
