---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-widget-data-layout
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Update Dynamic Widget Title
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/desktop-widget-data-layout). [Full Markdown](../../../../docs/desktop-widget-data-layout.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Connect custom widgets to Desktop data through STORE properties and JSON layout configuration.

## Selected section

## Update Dynamic Widget Title

Updates the wrapper title using the JavaScript SDK for the dynamic web component widget.

**Example**

```javascript
const e = new CustomEvent("unique-id-to-update-title", {
  bubbles: true,
  detail: {
    title: "new title"
  }
});
window.dispatchEvent(e);
```

In the CustomEvent, ensure that you use the same unique identifier (unique-id-to-update-title) specified in the JSON desktop layout. For more information on JSON layout, see [Create custom desktop layout](https://help.webex.com/en-us/article/ng08gqeb/Create-custom-desktop-layout) in Webex Help Center.

To update the iframe-based widget title, the iframe must share Desktop’s origin: the same scheme, hostname, and port.

**Example**

```html
<button id="customEvent" type="button">New Title</button>
<script>
  // This iframe must have the same origin as Desktop.
  // Match the event name configured in the Desktop layout.
  const titleEventName = "unique-id-to-update-title";
  document.querySelector("#customEvent").addEventListener("click", () => {
    const event = new window.parent.CustomEvent(titleEventName, {
      bubbles: true,
      detail: { title: "new title" }
    });
    window.parent.dispatchEvent(event);
  });
</script>
```
