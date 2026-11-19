---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-finesse-migration
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Migrate JavaScript Based Finesse Gadgets
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/desktop-finesse-migration). [Full Markdown](../../../../docs/desktop-finesse-migration.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Migrate embedded Finesse applications and refactor JavaScript gadgets into Desktop widgets.

## Selected section

## Migrate JavaScript Based Finesse Gadgets

There is no straightforward migration from a Shindig based gadget to a `wxcc-desktop` based widget. As the Shindig gadget and the `wxcc-desktop` widget leverage technologies, you can refactor the existing source code to develop `wxcc-desktop` based widgets. Finesse gadgets are based on the Apache Shindig gadget specification. For more information on Apache Shindig, see https://shindig.apache.org/. You can use any JavaScript library, framework, or our vanilla JavaScript to build a UI based gadget. The final content must be embedded within the gadget XML or HTML.

### Finesse Gadgets

Static Resources—Finesse gadgets consist of building blocks such as XML, HTML, CSS, JavaScript, and images. The gadgets are deployed in the Finesse 3rdpartygadget web application.

Elements—The following are the important elements of a gadget:

- The `<Module>` tag indicates that the XML file contains a gadget which is a root level element.
- The `<ModulePrefs>` tag contains information about the gadget. The tag includes the title, description, author, other optional features, and configuration related to the gadget from the Finesse desktop container.
- The `<Content type="html">` header tag indicates that the gadget's content type is HTML. The tag includes all markup content (HTML) and static resources that are embedded within the content element.

**Example: Sample Gadget**

```xml
<Module>
    <ModulePrefs title="X-Counter" description="X-Counter Example"></ModulePrefs>
    <Content type="html">
        <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css"/>
        <script src="https://cdnjs.cloudflare.com/ajax/libs/moment.js/2.29.1/moment.min.js"></script>
        <![CDATA[
    <style>
        button, p {
          display: inline-block;
        }
    </style><button aria-label="decrement">-</button><p>0</p><button aria-label="increment">+</button><script>
        var valueElement = document.querySelector('p');
        function increment() {
            const value = valueElement.innerText;
            valueElement.innerText = parseInt(value) + 1;
        }
        function decrement() {
            const value = valueElement.innerText;
            valueElement.innerText = parseInt(value) - 1;
        }
        var incrementButton = document.querySelectorAll('button')[1];
        var decrementButton = document.querySelectorAll('button')[0];

        incrementButton.addEventListener('click', () => increment());

        decrementButton.addEventListener('click', () => decrement());
    </script>
    ]]>
    </Content>
</Module>
```

For more information on Cisco Finesse gadgets, see https://developer.cisco.com/docs/finesse/#!finesse-overview/cisco-finesse-gadgets-finesse-javascript-library-api.

### Webex Contact Center Desktop Widgets

Desktop widget is based on the micro-frontend approach that leverages the browser's native Web Component module.

Static Resources—Custom widgets must bundle all their static resources (CSS, JavaScript, markup, and images) in a single JavaScript file using a bundle library (for example, Webpack, Rollup, Parcel). The bundle must be hosted in a Content Delivery Network (CDN). Custom widgets can use any JavaScript framework to develop Web Components.

Shared Data from Desktop (for example, ModulePrefs)—Custom widgets can have shared data or configuration from Desktop as a Web Component property or attributes.

**Note:** Desktop shared data or configuration is different from Finesse gadget shared data or configuration. The developer must understand the relevant shared data or configuration that are available in`wxcc-desktop`. For more information, see [Data Provider—Widget Properties and Attributes](https://developer.webex.com/docs/desktop-widget-data-layout#data-providerwidget-properties-and-attributes).

The JavaScript bundle must have the root element as Web Component, and the element name must be mentioned within the desktop layout configuration. Custom widgets can be developed using any web-based library or framework, for example, React, Angular, or Web Component. Custom widgets can also load additional static resources such as CSS, JavaScript, Markup, and images internally using Ajax or markup tags (script, link, img, and so on).

The following is an example of the sample Hello World widget without any bundling library (helloworld.js) and build using vanilla JavaScript. The widget name is `<x-counter>`.

**Example: Sample Widget Without Any Bundling Library**

```javascript
const template = document.createElement("template");
template.innerHTML = `
  <style>
    button, p {
      display: inline-block;
    }
  </style>
  <button aria-label="decrement">-</button>
    <p>0</p>
  <button aria-label="increment">+</button>
`;

class XCounter extends HTMLElement {
  increment() {
    const value = this.valueElement.textContent;
    this.valueElement.textContent = Number.parseInt(value, 10) + 1;
  }
  decrement() {
    const value = this.valueElement.textContent;
    this.valueElement.textContent = Number.parseInt(value, 10) - 1;
  }
  constructor() {
    super();

    this.attachShadow({
      mode: "open"
    });
    this.shadowRoot.appendChild(template.content.cloneNode(true));

    this.valueElement = this.shadowRoot.querySelector("p");
    this.incrementButton = this.shadowRoot.querySelectorAll("button")[1];
    this.decrementButton = this.shadowRoot.querySelectorAll("button")[0];

    this.incrementButton.addEventListener("click", () => this.increment());

    this.decrementButton.addEventListener("click", () => this.decrement());
  }
}

customElements.define("x-counter", XCounter);
```
