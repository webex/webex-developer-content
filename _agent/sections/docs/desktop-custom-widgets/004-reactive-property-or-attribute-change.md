---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-custom-widgets
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Reactive Property or Attribute Change
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/desktop-custom-widgets). [Full Markdown](../../../../docs/desktop-custom-widgets.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Build and test Web Components and iframe widgets for Webex Contact Center Desktop.

## Selected section

## Reactive Property or Attribute Change

Observe scalar layout attributes with `observedAttributes` and `attributeChangedCallback()`. The scalar property setters below reflect to those observed attributes, so property and attribute updates both render. For values supplied as JavaScript properties, such as arrays and objects, use a property setter that updates the component. `attributeChangedCallback()` does not run when a property is assigned. For more information, see [MDN documentation](https://developer.mozilla.org/en-US/docs/Web/Web_Components/Using_custom_elements).

The following example renders when the element connects, an observed attribute changes, or the `options` property is assigned. To update an array, assign a new array to `options`; mutating the existing array does not invoke its setter.

```javascript
class MyCustomElement extends HTMLElement {
  constructor() {
    super();
    this.attachShadow({ mode: "open" });
    this._options = [];
  }

  static get observedAttributes() {
    return ["width", "height", "active"];
  }

  get width() {
    return this.getAttribute("width") ?? "100px";
  }

  set width(value) {
    if (typeof value === "string") this.setAttribute("width", value);
    else this.removeAttribute("width");
  }

  get height() {
    return this.getAttribute("height") ?? "100px";
  }

  set height(value) {
    if (typeof value === "string") this.setAttribute("height", value);
    else this.removeAttribute("height");
  }

  get active() {
    return this.getAttribute("active") === "true";
  }

  set active(value) {
    this.setAttribute("active", String(value === true));
  }

  get options() {
    return this._options;
  }

  set options(value) {
    this._options = Array.isArray(value) ? value : [];
    this.render();
  }

  connectedCallback() {
    this.render();
  }

  attributeChangedCallback(name, oldValue, newValue) {
    if (oldValue !== newValue) this.render();
  }

  render() {
    if (!this.isConnected) return;
    const output = document.createElement("p");
    output.textContent = JSON.stringify({
      width: this.width,
      height: this.height,
      active: this.active,
      options: this.options
    });
    this.shadowRoot.replaceChildren(output);
  }
}

customElements.define("my-custom-element", MyCustomElement);
```
