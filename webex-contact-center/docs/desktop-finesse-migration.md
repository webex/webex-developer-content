---
type: Guide
title: Migrate Finesse Gadgets
display_title: Migrate Finesse Gadgets
canonical_url: https://developer.webex.com/docs/desktop-finesse-migration
content_type: documentation
product_group:
- webex-contact-center
categories:
- webex-contact-center
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/desktop-finesse-migration)

Migrate embedded Finesse applications and refactor JavaScript gadgets into Desktop widgets.

## Migrate Finesse Embedded Web Application Gadgets

You can migrate a Finesse embedded web application gadget into a Webex Contact Center Desktop iFrame based widget.

**Note:** Conversion of a Finesse gadget depends on the web application configuration-whether it could be loaded in an iFrame or not.

### Finesse—Embedded Web Application Sample Gadget

The embedded web application sample gadget displays a web page in an iFrame within the gadget. It is intended to serve as an example of placing an external web application in the Finesse gadget.

For more information on the embedded web application sample gadget, see https://github.com/CiscoDevNet/finesse-sample-code/tree/master/EmbeddedWebAppSampleGadget.

### Webex Contact Center Desktop—agentx-wc-iframe

Desktop has the inbuilt functionality (Web Component) to load web applications in an iFrame. Using the component `agentx-wc-iframe` within the desktop layout, you can load web applications in the horizontal header, navigation bar, and auxiliary information pane.

For more information on Webex Contact Center Desktop widgets, see https://github.com/CiscoDevNet/webex-contact-center-widget-starter/tree/master/Examples.

The following are the Finesse embedded gadget files:

- EmbeddedWebApp.css
- EmbeddedWebApp.js
- EmbeddedWebApp.xml

The EmbeddedWebApp.xml is the main file that contains the URL of the web application. Replace `https://widget.example.com/embedded-app` in every example with your controlled application URL. Its response must permit framing by your approved Desktop origins, as described in [iframe widget CSP configuration](https://developer.webex.com/docs/desktop-custom-widgets#iframe-widgets).

**Before you begin**

Understand the `script type` details from the Finesse embedded gadget file EmbeddedWebApp.xml.

```html
<script type="text/javascript">
    // initialize the gadget running the init handler defined in EmbeddedWebApp.js
    gadgets.HubSettings.onConnect = function () {
        finesse.modules.EmbeddedWebAppGadget.init("https://widget.example.com/embedded-app");
    };
</script>
```

Understand the JSON layout format. For more information on JSON layout, see [Create custom desktop layout](https://help.webex.com/en-us/article/ng08gqeb/Create-custom-desktop-layout) in Webex Help Center.

**Procedure**

Step 1: Access the JSON layout file from the Webex Contact Center Management Portal.

Step 2: In the `comp` property tag, enter the component value as `agentx-wc-iframe`.

```json
{
    "comp": "agentx-wc-iframe"
}
```

Step 3: In the `src attributes` property tag, enter the URL of the web application.

```json
{
    "comp": "agentx-wc-iframe",
    "attributes": {
        "src": "https://widget.example.com/embedded-app"
    }
}
```

Step 4: In the `wrapper` property tag, enter the title and the maximize area name.

```json
{
    "comp": "agentx-wc-iframe",
    "attributes": {
        "src": "https://widget.example.com/embedded-app"
    },
    "wrapper": {
        "title": "AgentX iFrame",
        "maximizeAreaName": "app-maximize-area"
    }
}
```

Step 5: Use the `style` property tag to resize the iFrame.

**Note:** The iFrame within the Desktop supports native iFrame properties.

```json
{
    "comp": "agentx-wc-iframe",
    "attributes": {
        "src": "https://widget.example.com/embedded-app"
    },
    "wrapper": {
        "title": "AgentX iFrame",
        "maximizeAreaName": "app-maximize-area"
    },
    "style": {
        "height": "504px",
        "width": "520px",
        "display": "inline-block",
        "align-items": "center"
    }
}
```

Step 6: Use the `attributes` property tag to add iFrame attributes.

```json
{
    "comp": "agentx-wc-iframe",
    "attributes": {
        "src": "https://widget.example.com/embedded-app",
        "sandbox": "allow-scripts allow-popups"
    },
    "wrapper": {
        "title": "AgentX iFrame",
        "maximizeAreaName": "app-maximize-area"
    },
    "style": {
        "height": "504px",
        "width": "520px",
        "display": "inline-block",
        "align-items": "center"
    }
}
```

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

## Related Pages

- [Agent Desktop overview](https://developer.webex.com/docs/desktop)
- [Desktop SDK Reference](https://developer.webex.com/docs/desktop-sdk-reference)

## Verify the Migration

Load the widget in Desktop and confirm that its title, size, and content match the layout. For the counter example, click both buttons and confirm that the displayed value changes. If an embedded application does not load, check its URL and framing policy. See [iframe requirements](https://developer.webex.com/docs/desktop-custom-widgets#iframe-widgets).
