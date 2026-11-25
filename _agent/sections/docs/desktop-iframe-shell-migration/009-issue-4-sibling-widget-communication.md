---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-iframe-shell-migration
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- 'Issue 4: Sibling Widget Communication'
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/desktop-iframe-shell-migration). [Full Markdown](../../../../docs/desktop-iframe-shell-migration.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Developer guidance for validating custom Desktop widgets, mitigating overlay clipping, refactoring host DOM dependencies, and communicating between sibling widgets.

## Selected section

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
