---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-custom-widgets
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Define Property or Attribute Interface
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/desktop-custom-widgets). [Full Markdown](../../../../docs/desktop-custom-widgets.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Build and test Web Components and iframe widgets for Webex Contact Center Desktop.

## Selected section

## Define Property or Attribute Interface

**Prerequisite:**
You must have an understanding of working with the Web Components and custom HTML elements. For more information, see [MDN documentation](https://developer.mozilla.org/en-US/docs/Web/Web_Components/Using_custom_elements).

Your custom element may extend the `HTMLElement` class or the one that inherits from `HTMLElement` class.

**Example**

```javascript
class MyCustomElement extends HTMLElement {
  constructor() {
    // Always call super first in constructor
    super();
    const shadow = this.attachShadow({
      mode: "open"
    });
    // write element functionality in here
  }
}
```

Assign property defaults in the constructor. These assignments create JavaScript properties and do not create DOM attributes. For attributes, parse the strings supplied by the layout and provide a fallback when an attribute is missing, as shown in the reactive example.

**Note:** DOM attributes contain strings. Pass Boolean values as properties, or explicitly parse an attribute value: the string `"false"` is truthy in JavaScript. The reactive example below treats only `active="true"` as active; a missing attribute or `active="false"` is inactive. For more information, see [Javascript.info](https://javascript.info/dom-attributes-and-properties).

**Example**

```javascript
class MyCustomElement extends HTMLElement {
  constructor() {
    // Always call super first in constructor
    super();
    const shadow = this.attachShadow({
      mode: "open"
    });

    this.width = "100px";
    this.height = "100px";
    this.active = false;

    // Data of types Array, Object, Map, Set, etc. cannot be passed as an attribute
    this.options = [];
  }
}
```
