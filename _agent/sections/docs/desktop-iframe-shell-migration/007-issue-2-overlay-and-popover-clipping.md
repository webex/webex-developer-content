---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-iframe-shell-migration
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- 'Issue 2: Overlay and Popover Clipping'
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/desktop-iframe-shell-migration). [Full Markdown](../../../../docs/desktop-iframe-shell-migration.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Developer guidance for validating custom Desktop widgets, mitigating overlay clipping, refactoring host DOM dependencies, and communicating between sibling widgets.

## Selected section

## Issue 2: Overlay and Popover Clipping

### What Happens

An iframe clips content at its boundary. A dropdown, menu, tooltip, popover, modal, drawer, or custom floating panel cannot visually extend outside the iframe, even if the widget uses CSS such as `overflow: visible`.

This behavior is enforced by the browser. It applies to Momentum UI, Material UI, custom `position: absolute` panels, nested iframes, and other floating UI patterns.

### How to Choose a Fix

Use this three-step path to choose the right mitigation:

1. **Confirm whether the widget opens floating UI.**
   If the widget does not open a dropdown, menu, tooltip, popover, modal, drawer, or similar panel, there is no overlay clipping risk. Validate normal rendering only.
   If the widget does open floating UI, continue to the placement check.
2. **Identify where the overlay trigger is placed.**
   If the trigger is in a panel, navigation area, sidebar, or another roomy slot, follow Fix 2A. The overlay can work if the iframe has enough width and height.
   If the trigger is in `advancedHeader` or another header slot, follow Fix 2B. Header iframes are too short for most overlays, so CSS overflow and slot sizing usually will not solve clipping.
3. **Validate at realistic window sizes.**
   Test the smallest Desktop window size the widget must support. If an overlay clips in a roomy slot, increase the widget slot size. If an overlay clips from a header slot, use the Desktop popover SDK or move the widget to a taller slot.

### Fix 2A: Overlay in a Roomy Slot

Use this approach for widgets in a panel, navigation area, sidebar, or another layout slot with enough width and height.

#### Recommended Action

Keep the widget in a layout area that gives it enough room to open its expected overlay content.

For example:

- Place the widget in its natural panel or navigation area instead of a thin strip.
- Configure a sensible minimum width and height for the widget slot.
- Confirm that typical dropdowns, menus, and comboboxes fit within the iframe.
- Test at production-realistic window sizes, including smaller Desktop windows.

This mitigation usually requires only layout configuration, not a widget code change.

#### Validation Guidance

Open every dropdown, menu, tooltip, popover, modal, and date picker in the widget and confirm that no floating content is clipped at the iframe edge. If clipping occurs, give the widget more room in its layout slot.

### Fix 2B: Overlay from a Header Slot

Use this approach when the widget or overlay trigger is placed in a header slot, such as:

- `area.advancedHeader[*]`
- `area.header.*`

Header slots are short, typically around the height of the Desktop header. Any overlay opened from that area is likely to extend beyond the iframe boundary. Increasing CSS overflow does not help, and slot sizing is usually not a practical fix.

#### Recommended Fixes

Choose one of the following approaches.

**1. Use the Desktop Popover SDK**

This is the preferred long-term fix for widgets that must remain in the header.

Instead of rendering the floating panel inside the widget iframe, the trigger widget calls `Desktop.popover.*`. The host Desktop renders the popover outside the widget iframe in a correctly sized and positioned panel.

Use this when:

- The widget must remain in the header.
- The widget opens a menu, dropdown, flyout, popover, or similar panel.
- You can update and re-publish the widget code.

**2. Move the Widget to a Roomier Slot**

If the widget does not have to remain in the header, move it to a panel, navigation area, sidebar, or another layout slot with enough space for the overlay.

Use this when:

- A configuration-only mitigation is preferred.
- Header placement is not essential.
- The widget cannot be updated quickly.

**3. Continue Legacy Rendering Temporarily If Directed**

For known affected header widgets, iframe shell enablement may remain disabled temporarily while a long-term mitigation is implemented. This avoids a user experience regression during migration.

This is not a replacement for updating the widget if the widget must eventually run in the iframe shell.



> **Example**
>
> Compare [`header-clip-widget`](https://github.com/CiscoDevNet/webex-contact-center-widget-starter/blob/master/Examples/Widgets/iframe-shell/src/header-clip-widget.ts) (`md-menu-overlay` clipped in the header) with [`header-popover-widget`](https://github.com/CiscoDevNet/webex-contact-center-widget-starter/blob/master/Examples/Widgets/iframe-shell/src/header-popover-widget.ts) (the same panel through `Desktop.popover`).



### Migrating a Header Widget to the Desktop Popover SDK

Use this pattern when a small header widget opens a larger floating panel.

#### Goal

Keep the header trigger inside the widget iframe, but render the larger panel through the Desktop popover SDK.

The result:

- The trigger remains in the header.
- The popover is positioned by Desktop.
- The popover is not clipped by the widget iframe.
- Desktop handles common dismissal behavior, such as outside click and Escape.

#### API Summary

| API | Called from | Purpose |
| --- | --- | --- |
| `await Desktop.popover.open(options)` | Trigger widget | Opens a popover and resolves with `{ popoverId }`. |
| `Desktop.popover.close()` | Trigger or popover content | Closes the current popover. |
| `Desktop.popover.isActive()` | Popover content | Returns `true` when the bundle is running inside the popover. |
| `Desktop.popover.resize({ width, height })` | Popover content | Resizes the popover after content loads or changes. |
| `Desktop.popover.onOpen(callback)` | Trigger widget | Registers an open handler and returns an unsubscribe function. |
| `Desktop.popover.onClose(callback)` | Trigger widget | Registers a close handler and returns an unsubscribe function. |

#### Important `open()` Options

| Option | Description |
| --- | --- |
| `comp` | Custom element tag name to load as popover content. |
| `script` | Script URL for the popover content bundle. This can be the same bundle as the trigger or a separate bundle. |
| `trigger.rect` | Anchor rectangle from the trigger button's `getBoundingClientRect()`. Pass this so Desktop can anchor the popover to the trigger. |
| `panel` | Popover sizing and placement options, such as `width`, `height`, `maxHeight`, `placement`, and `offset`. |
| `properties` | Properties forwarded to the popover content element. |
| `attributes` | Attributes forwarded to the popover content element. |
| `dismissOn` | Dismissal options such as outside click, Escape, window resize, or window blur. |

#### Migration Steps

1. **Separate the trigger from the content.**
   Keep the small button or icon in the header widget. Move the larger panel UI into popover content. The content can live in the same bundle or in a separate bundle.
2. **Replace local overlay rendering.**
   Replace code that renders an `md-menu-overlay`, Material UI popover, or custom absolute-positioned panel with a call to `Desktop.popover.open()`.
3. **Pass the trigger rectangle.**
   Use the trigger button's `getBoundingClientRect()` and pass it as `trigger.rect` so the popover anchors to the button.
4. **Forward layout inputs the content needs.**
   Layout `attributes` and `properties` apply only to the trigger widget. The popover content receives only the `attributes` and `properties` passed to `Desktop.popover.open()`, so forward any configuration the panel depends on.
5. **Remove custom positioning and dismiss logic.**
   Desktop handles placement, flip and clamp behavior, outside click, Escape, scroll, and resize. Use `dismissOn` only when you need to tune the defaults.
6. **Resize from the popover content if needed.**
   If the content changes after loading, call `Desktop.popover.resize()`.
7. **Close the popover when the user completes an action.**
   Call `Desktop.popover.close()` from the content or trigger.
8. **Reflect open and closed state in the trigger.**
   Use `Desktop.popover.onOpen()` and `Desktop.popover.onClose()` to update active styling, badges, or other trigger state. Unsubscribe in `disconnectedCallback()`.
9. **Keep backgrounds transparent when appropriate.**
   Use `:host { background: transparent; }` for trigger and content elements when you want Desktop theming to show through.

#### Example

This example uses one bundle for both the header trigger and the popover content. It initializes the Desktop SDK, then branches on `Desktop.popover.isActive()`. Replace the `script` URL with the absolute URL of your bundle, the same URL you use in the layout. The `tenant-id` attribute and `config` property stand for whatever layout values your panel needs; forward them in the `open()` call.

```javascript
import { Desktop } from "@wxcc-desktop/sdk";

class VendorWidget extends HTMLElement {
  connection = 0;

  async connectedCallback() {
    const connection = ++this.connection;
    this.sdkReady = Desktop.config.init({ widgetName: "vendor-widget", widgetProvider: "vendor" });
    await this.sdkReady;

    // Desktop can disconnect, or disconnect and reconnect, the widget while init() is pending.
    if (connection !== this.connection) {
      return;
    }

    if (Desktop.popover.isActive()) {
      this.renderPanel();
    } else {
      this.renderTrigger();
    }
  }

  renderTrigger() {
    this.innerHTML = `<button>Stats</button>`;
    const button = this.querySelector("button");

    this.offClose = Desktop.popover.onClose(() => {
      button.classList.remove("active");
    });

    button.addEventListener("click", async () => {
      const rect = button.getBoundingClientRect();

      const result = await Desktop.popover.open({
        comp: "vendor-widget",
        script: "https://widget.example.com/widgets/vendor.js",
        // Layout values reach only the trigger; the panel gets only what is passed here.
        attributes: { "tenant-id": this.getAttribute("tenant-id") },
        properties: { config: this.config },
        trigger: {
          rect: {
            x: rect.left,
            y: rect.top,
            width: rect.width,
            height: rect.height
          }
        },
        panel: {
          width: "420px",
          maxHeight: "560px",
          placement: "bottom-end"
        }
      });

      if (result?.popoverId) {
        button.classList.add("active");
      }
    });
  }

  renderPanel() {
    this.innerHTML = `<div>Rich content</div>`;

    // Call this if content size changes after initial render.
    // Desktop.popover.resize({ height: "auto" });

    // Call this after the user completes the popover action.
    // Desktop.popover.close();
  }

  disconnectedCallback() {
    const connection = ++this.connection;
    this.offClose?.();
    this.offClose = undefined;

    this.sdkReady?.then(() => {
      // Skip cleanup if the widget reconnected and a newer connection owns the SDK.
      if (connection === this.connection) {
        Desktop.config.cleanup();
      }
    });
  }
}

customElements.define("vendor-widget", VendorWidget);
```



> **Example**
>
> For a complete TypeScript version with an in-page fallback, see [`header-popover-widget.ts`](https://github.com/CiscoDevNet/webex-contact-center-widget-starter/blob/master/Examples/Widgets/iframe-shell/src/header-popover-widget.ts). For a production-style widget migrated the same way, see [`notes-header-widget`](https://github.com/CiscoDevNet/webex-contact-center-widget-starter/tree/master/Examples/Widgets/Notes).



#### Additional Notes

- Re-clicking the trigger while its popover is open closes it. The iframe shell treats a second `Desktop.popover.open()` call with the same `trigger.rect` as a close, so the example needs no separate close branch. That call resolves with the closing popover's `popoverId`, and `onClose` fires shortly after to clear the trigger's active state. If the trigger has moved since the popover opened, the call opens a new popover instead.
- Only one Desktop popover is active at a time. Opening a new popover closes the previous one.
- If the popover content embeds its own iframe, automatic Escape handling, outside-click detection, theming, and SDK plumbing do not reach inside that nested iframe. Bridge those events with `postMessage` and call `Desktop.popover.close()` from your content widget.
- For full option defaults, the complete API surface, and additional examples, see [Popovers](https://developer.webex.com/docs/desktop-popovers).
