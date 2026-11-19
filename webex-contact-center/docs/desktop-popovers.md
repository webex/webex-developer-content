---
type: Guide
title: Popovers
display_title: Popovers
canonical_url: https://developer.webex.com/docs/desktop-popovers
content_type: documentation
product_group:
- webex-contact-center
categories:
- webex-contact-center
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/desktop-popovers)

Open, position, resize, and dismiss popovers within the isolated Desktop widget sandbox.

## Before You Begin

Install and initialize the SDK as described in [Get Started with the Desktop SDK](https://developer.webex.com/docs/desktop-sdk-getting-started). Your widget must run inside Webex Contact Center Desktop.

## Popover Module

The `Desktop.popover` module lets your custom widget open a floating popover panel anchored to a trigger element in your widget. Desktop renders your popover content, positions it, keeps it anchored while the page scrolls or resizes, and dismisses it automatically—so you can offer a compact trigger (for example, a button in the header) that expands into a richer panel on demand.

Typical use cases:

- A small trigger in a space-constrained slot that expands into a larger panel.
- Popover content that lives in a separate bundle from the trigger.
- A panel that should automatically close on outside click, Escape, or when the trigger scrolls out of view.



> **Availability**
>
> The popover APIs are available only to custom widgets that run inside the isolated (sandboxed) environment Webex Contact Center Desktop provides for custom widgets. If your widget isn't running in that environment, these methods have no effect and log a warning (`open()` resolves to `undefined`). Always initialize the SDK with `Desktop.config.init({ widgetName: "my-widget", widgetProvider: "cisco" })` before calling popover methods.



**Note:** Only one popover can be open at a time. Opening a new popover automatically closes the previous one.

### Methods

#### open(options)

Opens a popover and renders the specified custom element inside it. Returns a promise that resolves to `{ popoverId }`, or `undefined` if the popover could not be opened.

**Example**

```javascript
import { Desktop } from "@wxcc-desktop/sdk";

class MyPopoverTrigger extends HTMLElement {
  constructor() {
    super();
    this.attachShadow({ mode: "open" });
    const button = document.createElement("button");
    button.textContent = "Open popover";
    this.shadowRoot.append(button);

    button.addEventListener("click", async () => {
      const rect = button.getBoundingClientRect();

      const result = await Desktop.popover.open({
        comp: "my-popover-content",              // custom element tag to render
        script: "https://example.com/popover.js", // bundle that defines that element
        panel: {
          width: "420px",
          maxHeight: "560px",
          placement: "bottom-end"
        },
        properties: {
          customerId: this.getAttribute("customer-id")
        },
        // Anchor the popover to the button, not the whole widget
        trigger: {
          rect: { x: rect.left, y: rect.top, width: rect.width, height: rect.height }
        }
      });

      if (result) {
        console.log("Popover opened:", result.popoverId);
      }
    });
  }
}

customElements.define("my-popover-trigger", MyPopoverTrigger);
```

**Parameters**

| Name | Type | Description | Required |
|------|------|-------------|----------|
| comp | string | Tag name of the custom element to render inside the popover. | Yes |
| script | string | URL of the bundle that defines `comp`. May differ from your trigger's bundle. | Yes |
| panel | Object | Popover panel appearance and placement. | No |
| -->width | string | CSS width of the popover. Default `"350px"`. | No |
| -->height | string | CSS height. Default `"auto"`. | No |
| -->maxHeight | string | CSS max-height; also clamped to the viewport. Default `"500px"`. | No |
| -->placement | string | Preferred placement; auto-flips when space is limited. Default `"bottom-start"`. | No |
| -->offset | number | Pixel gap between the trigger and the popover. Default `4`. | No |
| attributes | Object | HTML attributes set on the popover element. | No |
| properties | Object | JS properties set on the popover element. | No |
| dismissOn | Object | Controls automatic dismissal (see Dismiss behavior). | No |
| trigger.rect | Object | The trigger element's position (`{ x, y, width, height }`) from `getBoundingClientRect()`. Omit to anchor to the whole widget. | No |

Supported `placement` values: `top-start`, `top`, `top-end`, `bottom-start`, `bottom`, `bottom-end`, `left-start`, `left`, `left-end`, `right-start`, `right`, `right-end`.

**Note:** Values from layout JSON apply to your trigger widget only. The popover content widget receives just the `attributes` and `properties` you pass to `open()`, so forward anything the popover needs.

#### close()

Closes the popover opened by your widget. Can be called from the trigger widget or from within the popover content.

```javascript
await Desktop.popover.close();
```

#### resize(dimensions)

Resizes the open popover. Typically called from within the popover content after it loads.

```javascript
await Desktop.popover.resize({ width: "520px", height: "auto" });
```

| Name | Type | Description | Required |
|------|------|-------------|----------|
| width | string | New CSS width. | No |
| height | string | New CSS height. | No |
| maxHeight | string | New CSS max-height. | No |

#### isActive()

Returns `true` when the current code is running **inside** a popover (that is, your widget was loaded as popover content). Use it to render different UI for the trigger versus the popover.

```javascript
if (Desktop.popover.isActive()) {
  this.renderPopoverContent();
} else {
  this.renderTrigger();
}
```

#### onOpen(callback) / onClose(callback)

Subscribe to popover lifecycle events. Each returns an unsubscribe function—call it in your widget's `disconnectedCallback` to avoid leaks.

```javascript
class PopoverWidget extends HTMLElement {
connectedCallback() {
  this.offOpen = Desktop.popover.onOpen(({ popoverId }) => {
    this.button.classList.add("active");
  });
  this.offClose = Desktop.popover.onClose(({ popoverId }) => {
    this.button.classList.remove("active");
  });
}

disconnectedCallback() {
  this.offOpen?.();
  this.offClose?.();
}
}
```

### Dismiss behavior

By default, the popover closes on outside click and on Escape. Override with the `dismissOn` option:

| Option | Default | Description |
|--------|---------|-------------|
| outsideClick | `true` | Close when the user clicks outside the popover. |
| escape | `true` | Close when the user presses Escape. |
| windowResize | `false` | Close when the browser window is resized. |
| windowBlur | `false` | Close when the window loses focus. |

```javascript
await Desktop.popover.open({
  comp: "my-popover-content",
  script: "https://example.com/popover.js",
  dismissOn: { outsideClick: true, escape: false }
});
```

Desktop also closes the popover automatically when the trigger scrolls out of view, is hidden, or is removed from the layout.

### Theming

The popover content receives an `isDarkTheme` property automatically so it can match the agent's current theme. To force a specific mode, pass it explicitly:

```javascript
await Desktop.popover.open({
  comp: "my-popover-content",
  script: "https://example.com/popover.js",
  properties: { isDarkTheme: false }
});
```

### Composition patterns

**Two bundles** — a trigger widget and a separate popover-content widget:

```javascript
// trigger.js
class MyTrigger extends HTMLElement {
  connectedCallback() {
    this.innerHTML = `<button>Open</button>`;
    this.querySelector("button").addEventListener("click", () => {
      Desktop.popover.open({
        comp: "my-popover-content",
        script: "https://example.com/popover.js"
      });
    });
  }
}
customElements.define("my-trigger", MyTrigger);

// popover.js
class MyPopoverContent extends HTMLElement {
  connectedCallback() {
    this.innerHTML = `<div>Rich content here…</div>`;
  }
}
customElements.define("my-popover-content", MyPopoverContent);
```

**Single bundle** — one widget that plays both roles by branching on `isActive()`:

```javascript
class MyWidget extends HTMLElement {
  connectedCallback() {
    if (Desktop.popover.isActive()) {
      this.innerHTML = `<div>Rich content here…</div>`;
    } else {
      this.innerHTML = `<button>Open</button>`;
      this.querySelector("button").addEventListener("click", () => {
        Desktop.popover.open({ comp: "my-widget", script: this.getBundleUrl() });
      });
    }
  }
}
customElements.define("my-widget", MyWidget);
```

### Limitations

- If your popover content embeds its own nested `<iframe>`, automatic dismissal (Escape, outside click, scroll) and theming do not apply to that nested frame. Handle those cases in your own code and call `Desktop.popover.close()` when needed.
- The `trigger.rect` coordinates must come from `getBoundingClientRect()` within your widget. Coordinates from a nested iframe are in a different coordinate space and won't anchor correctly.

## Related Pages

- [Agent Desktop overview](https://developer.webex.com/docs/desktop)
- [Desktop SDK Reference](https://developer.webex.com/docs/desktop-sdk-reference)
