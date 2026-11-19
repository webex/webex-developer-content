---
type: Guide
title: Migrate Custom Widgets to the Secure Iframe Shell
display_title: Migrate Custom Widgets to the Secure Iframe Shell
canonical_url: https://developer.webex.com/docs/desktop-iframe-shell-migration
content_type: documentation
product_group:
- webex-contact-center
categories:
- webex-contact-center
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/desktop-iframe-shell-migration)

Developer guidance for validating custom Desktop widgets, mitigating overlay clipping, refactoring host DOM dependencies, and communicating between sibling widgets.

## Overview

This guide explains what changes in the new runtime model, which widget behaviors require validation or code changes, and how to update widgets that rely on overlays, host-page DOM access, or events shared with other widgets.

Webex Contact Center Desktop is moving custom widgets into an iframe shell. In the legacy model, a widget runs directly inside the Desktop page and shares the same document as the host application. In the iframe shell model, each widget runs in its own isolated iframe document—with its own DOM and its own browser storage (`localStorage`, `sessionStorage`, and cookies) separate from the host application.

This isolation improves stability and security, but it changes how widgets interact with shared page resources:

| Area | What changes | Required action |
| --- | --- | --- |
| Momentum UI `md-*` components | Momentum UI is made available inside the iframe shell. | No code change required. Confirm the widget renders correctly. |
| Floating overlays | Dropdowns, menus, tooltips, popovers, dialogs, and similar UI cannot render outside the iframe boundary. | Test all overlays. Increase the widget slot size when possible, or use the Desktop popover SDK for header widgets. |
| Host DOM access | A widget can no longer query or manipulate DOM elements owned by the host Desktop page or by sibling widgets. | Refactor the widget to use supported APIs and keep DOM access inside the widget's own subtree. |
| Host storage and cookies | A widget can no longer read or write the host Desktop application's `localStorage`, `sessionStorage`, or cookies (or another widget's storage). | Get host and agent data from the supported Desktop SDK instead of host storage. Keep storage within your own widget. |
| Sibling widget communication | Each widget has its own `window`. `CustomEvent`s, `window` events, and shared globals no longer reach other widgets. | Send data to sibling widgets with `postMessage`. Desktop relays the message between widget iframes. |



> **Working examples**
>
> The [Webex Contact Center widget starter](https://github.com/CiscoDevNet/webex-contact-center-widget-starter/tree/master/Examples/Widgets/iframe-shell) has small widgets that show each issue in this guide in its broken and fixed form, with source code. See [Try the Iframe Shell Examples](#try-the-iframe-shell-examples).



## Who Should Use This Guide

Use this guide if you build, configure, or maintain a Webex Contact Center Desktop custom widget that will run in the iframe shell.

This guide is especially relevant if your widget:

- Uses Momentum UI `md-*` components.
- Opens floating UI, such as dropdowns, menus, tooltips, popovers, dialogs, or custom panels.
- Is placed in a header slot, such as `area.advancedHeader[*]` or `area.header.*`.
- Reads or modifies Desktop host DOM or another widget's DOM.
- Sends or listens for events or data shared with another widget.

## Quick Guidance

Most widgets do not require changes. The iframe shell provides Momentum UI, proxies the Desktop SDK, and relays supported events.

You may need to act if your widget does any of the following:

- Opens floating UI, such as dropdowns, menus, tooltips, comboboxes, date pickers, modals, dialogs, or custom absolute-positioned panels.
- Opens an overlay from a header slot, such as `area.advancedHeader[*]` or `area.header.*`.
- Reads or modifies DOM elements that the widget did not create, including host Desktop elements or elements inside another widget.
- Uses `CustomEvent`, `window` events, shared globals, or shared storage to pass data to another widget.

If your widget only uses inline controls, such as buttons, inputs, labels, icons, checkboxes, spinners, tabs, avatars, or badges, you generally only need to validate that the widget renders correctly in the iframe shell. If the widget is in a header slot, also confirm its width. See Header widget width in [Impact Categories](#impact-categories).

## Impact Categories

| Category | Applies when | Primary action | Example |
| --- | --- | --- | --- |
| Momentum UI components | The widget uses Momentum UI `md-*` components that previously relied on the host page. | Confirm rendering. Test overlays if the widget uses overlay-prone components. | — |
| Header overlay risk | The widget opens floating UI from a header or `advancedHeader` slot. | Use the Desktop popover SDK or move the widget to a roomier slot. | [`header-clip-widget`](https://github.com/CiscoDevNet/webex-contact-center-widget-starter/blob/master/Examples/Widgets/iframe-shell/src/header-clip-widget.ts), [`header-popover-widget`](https://github.com/CiscoDevNet/webex-contact-center-widget-starter/blob/master/Examples/Widgets/iframe-shell/src/header-popover-widget.ts) |
| Header widget width | The widget renders in a header or `advancedHeader` slot. | Size the widget from its content, such as `display: inline-flex; width: max-content`. Do not use `width: 100%`. Confirm the widget is neither truncated nor wider than its content. | [`header-fit-widget`](https://github.com/CiscoDevNet/webex-contact-center-widget-starter/blob/master/Examples/Widgets/iframe-shell/src/header-fit-widget.ts), [`header-overflow-widget`](https://github.com/CiscoDevNet/webex-contact-center-widget-starter/blob/master/Examples/Widgets/iframe-shell/src/header-overflow-widget.ts) |
| Host DOM access | The widget queries or manipulates host Desktop DOM or another widget's DOM. | Refactor the widget to stop depending on DOM it did not create. | [`sdk-init-widget`](https://github.com/CiscoDevNet/webex-contact-center-widget-starter/blob/master/Examples/Widgets/iframe-shell/src/sdk-init-widget.ts) |
| Sibling widget communication | The widget sends data to, or receives data from, another widget. | Replace `CustomEvent`s and shared globals with `postMessage`. | [`sibling-bus-publisher`](https://github.com/CiscoDevNet/webex-contact-center-widget-starter/blob/master/Examples/Widgets/iframe-shell/src/sibling-bus-publisher.ts), [`sibling-bus-consumer`](https://github.com/CiscoDevNet/webex-contact-center-widget-starter/blob/master/Examples/Widgets/iframe-shell/src/sibling-bus-consumer.ts) |

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

## Issue 3: Host DOM Access

### What Happens

In the legacy model, a widget could sometimes access the host Desktop DOM because it shared the same document. For example, a widget might:

- Call `document.querySelector("agentx-app")`.
- Traverse a host element's `shadowRoot`.
- Attach listeners to host controls.
- Read or modify another widget's DOM.

In the iframe shell model, the widget can only access its own iframe document. Host elements and sibling widget elements are outside the iframe boundary.

### Required Action

Refactor the widget so it does not depend on DOM elements it did not create.

There is no supported host DOM shim or stand-in element for the Desktop page. Treat the widget iframe as the only DOM the widget is allowed to query or mutate.

### Refactoring Guidance

Use these rules when updating the widget:

- Remove selectors that target host Desktop elements or sibling widgets.
- Do not walk into another component's `shadowRoot`.
- Get agent and Desktop state from the supported Desktop SDK instead of scraping the host UI.
- Subscribe to supported SDK events instead of intercepting clicks on host controls.
- Keep DOM queries scoped to elements rendered by the widget.
- Degrade gracefully if optional data is not available.
- Use `postMessage` for supported communication between sibling widget iframes instead of reading another widget's DOM. See [Issue 4: Sibling Widget Communication](#issue-4-sibling-widget-communication).

**Rule of thumb:** if the widget touches an element it did not create, that code needs an iframe-safe refactor.



> **Example**
>
> [`sdk-init-widget`](https://github.com/CiscoDevNet/webex-contact-center-widget-starter/blob/master/Examples/Widgets/iframe-shell/src/sdk-init-widget.ts) starts with `Desktop.config.init()` and reads agent data from the SDK instead of calling `document.querySelector("agentx-app")`.



## Issue 4: Sibling Widget Communication

### What Happens

In the legacy model, widgets on the same Desktop page shared one `window` and one `document`. Widgets often passed data to each other by:

- Dispatching a `CustomEvent` on `window`, `document`, or a shared element.
- Setting or reading a global variable on `window`.
- Writing to `localStorage` or `sessionStorage` and reading it in another widget.
- Calling methods on another widget's element.

In the iframe shell model, each widget has its own iframe, `window`, `document`, and storage. A `CustomEvent`—even with `bubbles: true` and `composed: true`—stays inside the sender's iframe. Globals and storage are not shared, and another widget's element is outside the iframe boundary.

### What the Iframe Shell Provides

Desktop relays `postMessage` between widget iframes. A message that a widget posts on its own `window` is delivered to its sibling widgets as a `message` event.

### Required Action

Replace cross-widget `CustomEvent`s, shared globals, shared storage, and direct element calls with `postMessage`.

### Refactoring Guidance

Use these rules when updating the widget:

- Send data with `window.postMessage()`, using an event `type` that you define.
- Make the `type` unique to your organization and widget, for example `"acme.crm:view-changed"`. Avoid generic names such as `"update"`, `"message"`, or `"event"`.
- Listen for the `message` event in the receiving widget, and handle only the types you defined. Desktop and the iframe shell post their own messages on the same channel; ignore them.
- Validate the shape of every message before using it.
- Treat every relayed message as untrusted. A unique `type` filters messages but does not identify the sender, because any widget on the page can post the same `type`. Before a message triggers sensitive behavior, such as opening a record or changing data, validate it and confirm authorization independently, for example through the Desktop SDK or your own backend.
- Keep `CustomEvent`s only for listeners inside the same widget.
- Get agent, task, and Desktop state from the Desktop SDK in each widget instead of forwarding it from another widget.
- Do not send sensitive information, such as access tokens, passwords, API keys, or other secrets, in a message. Treat message payloads as visible to every widget on the page.



> **Caution**
>
> A message sent with `window.postMessage()` is delivered to **every** widget on the Desktop page, not only the one you intend. Every widget that listens for `message` receives it, including widgets from other vendors. Use a unique event `type`, check the `type` before acting on a message, and ignore anything you do not recognize. Two widgets that use the same generic `type` will receive and may act on each other's messages. A unique `type` does not prove which widget sent a message.



### Example

This example uses `"acme.crm:view-changed"` as a user-defined event type. Replace it with a type unique to your widget.

Sender:

```javascript
window.postMessage(
  {
    type: "acme.crm:view-changed",
    view: "history"
  },
  "*"
);
```

Receiver:

```javascript
class VendorConsumer extends HTMLElement {
  connectedCallback() {
    this.onMessage = (event) => {
      const data = event.data;
      if (!data || data.type !== "acme.crm:view-changed") {
        return; // not ours: Desktop, the iframe shell, or another widget
      }
      if (typeof data.view === "string") {
        this.showView(data.view);
      }
    };
    window.addEventListener("message", this.onMessage);
  }

  disconnectedCallback() {
    window.removeEventListener("message", this.onMessage);
  }
}
```



> **Example**
>
> [`sibling-bus-publisher`](https://github.com/CiscoDevNet/webex-contact-center-widget-starter/blob/master/Examples/Widgets/iframe-shell/src/sibling-bus-publisher.ts) sends the same payload once as a `CustomEvent` (never arrives) and once with `postMessage` (relayed). The starter uses its own event type for this demo; use a type unique to your widget. [`sibling-bus-consumer`](https://github.com/CiscoDevNet/webex-contact-center-widget-starter/blob/master/Examples/Widgets/iframe-shell/src/sibling-bus-consumer.ts) listens for both. The [Timer widget](https://github.com/CiscoDevNet/webex-contact-center-widget-starter/tree/master/Examples/Widgets/Timer) posts a `timer-expired` message the same way.



## Widgets With Multiple Issues

Some widgets may be affected by more than one iframe shell behavior. Use this order of operations:

- If the widget opens an overlay from a header slot, address the header overlay issue first. Momentum UI rendering and slot sizing alone will not prevent header overlay clipping.
- If the widget also accesses host or sibling DOM, complete the host DOM refactor before go-live.
- If the widget passes data to other widgets, move that communication to `postMessage` before go-live.
- After code or layout changes, run the full testing checklist against the final iframe shell configuration.

## Testing Checklist

Run this checklist after enabling the widget in the iframe shell.

1. Note the widget script URL, layout slot, and whether it uses Momentum UI components, floating overlays, host DOM access, or sibling widget communication.
2. To see expected iframe shell behavior first, run the sample layout in [Try the Iframe Shell Examples](#try-the-iframe-shell-examples). Load your widget from an absolute `script` URL.
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

## FAQ

### Can my widget still access the Desktop application's browser storage?

No. Your widget now runs in its own isolated origin, so it can't read or write the host application's storage or cookies (this worked before only because the widget shared the host page). Get host and agent data from the supported Desktop SDK, and use `postMessage` to share data with sibling widgets.

### Do I need to bundle Momentum UI for the iframe shell?

No. The iframe shell registers Momentum UI inside the widget iframe, so existing `md-*` markup can continue to render without bundling Momentum UI in the widget.

### Will inline Momentum components break?

Inline components such as `md-button`, `md-input`, `md-icon`, and `md-checkbox` are expected to continue working. They render within the widget's own area, so they do not have the same iframe-boundary clipping risk as overlays.

### What is the main risk for Momentum UI widgets?

The main risk is clipping for floating UI. Test every component that opens a dropdown, menu, tooltip, popover, date picker, modal, or similar panel inside the iframe shell.

### Can CSS `overflow: visible` fix iframe clipping?

No. Browser iframe boundaries clip their contents. Setting CSS `overflow: visible` does not allow widget content to render outside the iframe.

### What should I do if my widget opens a menu from the header?

Use the Desktop popover SDK for the menu content or move the widget to a taller layout slot. Header slots are too short for most floating UI, so resizing or CSS overflow usually will not solve the issue.

### How do I anchor a Desktop popover to my trigger button?

Call `getBoundingClientRect()` on the trigger button and pass the resulting coordinates as `trigger.rect` in `Desktop.popover.open()`. This lets Desktop position the popover relative to the actual trigger, not just the widget frame.

### Which Desktop SDK version includes `Desktop.popover`?

`Desktop.popover` is available in [`@wxcc-desktop/sdk` 3.0.1](https://www.npmjs.com/package/@wxcc-desktop/sdk/v/3.0.1) and later. Earlier versions do not include it. Install it with `npm install @wxcc-desktop/sdk@^3.0.1`. The popover methods work only when the widget runs in the iframe shell; elsewhere they do nothing and `open()` resolves without a `popoverId`.

### How do I know whether my widget needs a host DOM refactor?

Search for code that queries or manipulates elements the widget did not create. Common examples include `document.querySelector()` calls targeting Desktop host elements, `getElementsByTagName()` calls for host elements, and `shadowRoot` traversal into host or sibling components. Replace those patterns with supported Desktop SDK APIs or message passing.

### Can sibling widgets communicate after iframe migration?

Yes, but they should communicate through supported message passing, such as `postMessage`. Do not read, mutate, or traverse another widget's DOM. See [Issue 4: Sibling Widget Communication](#issue-4-sibling-widget-communication).

### Do I need to test every deployment that uses the same widget bundle?

Test each unique combination of script URL, layout slot, and layout `attributes` and `properties`. Deployments that match on all of these can share one validation pass. Desktop applies a deployment's attributes and properties to the widget element inside the iframe, so different values can change what the widget renders and which overlays it opens.

### Are there working examples I can run?

Yes. The [widget starter iframe shell examples](https://github.com/CiscoDevNet/webex-contact-center-widget-starter/tree/master/Examples/Widgets/iframe-shell) show header popover, header clipping, sibling communication, and SDK initialization without host DOM. Follow [Try the Iframe Shell Examples](#try-the-iframe-shell-examples) to run them in Desktop.

### Why does my `CustomEvent` no longer reach another widget?

Each widget has its own iframe and `window`. A `CustomEvent`, even with `bubbles` and `composed`, stays inside the sender's iframe. Send the data with `window.postMessage()` and listen for `message` in the other widget.

### Do I need to know where a sibling widget is placed to send it a message?

No. Post the message on your own `window`. Desktop relays it to the other widget iframes, whether they are in the header, navigation, panel, or headless area. Because every widget receives it, give the message a unique `type` and check that `type` in the receiver.

### Can I send tokens or other secrets with `postMessage`?

No. Treat widget bundles, layout JSON, and message payloads as visible to every widget on the page. Load credentials from your own server or the customer's secret store.

### Can I pass `$STORE`, `$STORE.agent`, or `$STORE.app` to my widget from the layout JSON?

No. In the legacy model this could work, because the widget shared the Desktop page and received the live store object directly. In the iframe shell, Desktop copies layout properties and attributes across the iframe boundary. Whole store objects such as `$STORE`, `$STORE.agent`, and `$STORE.app` contain functions and live, observable state, which cannot be copied, so the widget no longer receives them.

`STORE.agent`, `STORE.agentContact`, `STORE.app`, and the other top-level keys are groups of values, not values to bind. Bind the specific documented paths your widget needs. For the full list of supported paths and their types, see [Widget Data and Desktop Layout](https://developer.webex.com/docs/desktop-widget-data-layout).

```json
{
    "comp": "vendor-widget",
    "script": "https://widget.example.com/widgets/vendor.js",
    "attributes": {
        "agent-id": "$STORE.agent.agentId"
    },
    "properties": {
        "isDarkTheme": "$STORE.app.darkMode"
    }
}
```

Use documented paths that resolve to strings, numbers, booleans, or plain data objects or arrays, such as `$STORE.agent.teamId` or `$STORE.agent.channelsStatesMap`. For anything else, call the Desktop SDK from the widget.

### Can I pass a callback function to my widget?

No. Functions cannot cross the iframe boundary, so a callback passed to the widget as a property or attribute does not reach it. Pass data values only. If the widget needs Desktop data or actions, call the Desktop SDK from inside the widget.

## Related Pages

- [Agent Desktop overview](https://developer.webex.com/docs/desktop)
- [Build Custom Widgets](https://developer.webex.com/docs/desktop-custom-widgets)
- [Popovers](https://developer.webex.com/docs/desktop-popovers)
- [Widget Data and Desktop Layout](https://developer.webex.com/docs/desktop-widget-data-layout)
- [Get Started with the Desktop SDK](https://developer.webex.com/docs/desktop-sdk-getting-started)
- [Desktop SDK Reference](https://developer.webex.com/docs/desktop-sdk-reference)
