---
type: Guide
title: Build Custom Widgets
display_title: Build Custom Widgets
canonical_url: https://developer.webex.com/docs/desktop-custom-widgets
content_type: documentation
product_group:
- webex-contact-center
categories:
- webex-contact-center
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/desktop-custom-widgets)

Build and test Web Components and iframe widgets for Webex Contact Center Desktop.

## Build a Custom Widget

The Webex Contact Center Desktop supports extensions in the form of widgets. Widgets are essential components for desktop customization. A widget is a component with some specific encapsulated functionality, exported as a custom HTML element that is placed within the desktop. We recommend these custom HTML elements to be Web Components also, because any widget ends up being placed inside a nested tree of Shadow Roots, and will require a Shadow Document Object Model (DOM) of its own to be enabled for styling encapsulation.

Learning that any widget for Webex Contact Center Desktop must be a Web Component or an embedded iFrame, a developer might feel forced into a technology. However, the developer can build these components on any compatible framework. For a widget integrated directly as a custom element, export it as a Web Component: wrap its functionality in a custom HTML element defined in the JavaScript bundle, with Shadow DOM enabled. An application embedded by URL in an iframe does not need to export a Web Component or enable Shadow DOM.

The following are a few examples for custom widgets:

- If you choose to build your widget in Angular JavaScript, make sure that your Angular version supports [Angular Elements](https://angular.io/guide/elements) (added in version 6), and your application is exported as an Angular Element.
- If you choose to build your application in React (similar to parts of Desktop), you can wrap your React application into a custom HTML element and enable Shadow DOM manually, or use some of the open-source solutions that automate this process for you. For example, [Direflow](https://direflow.io/).
- There are various other frameworks that are fully prepared to consume Web Components and be exported as Web Components. For reference, you can use https://custom-elements-everywhere.com that regularly runs automated tests against popular frameworks to check their ongoing compatibility.

You do not have to use a framework to build a web application to be exported as a widget. In fact, all examples in this documentation reference vanilla JavaScript.

The following are the different types of custom widgets:

- Header widgets
- Navigation (custom page) widgets
- Persistent widgets
- Headless widgets

For more information on custom widgets, see [Create custom desktop layout](https://help.webex.com/en-us/article/ng08gqeb/Create-custom-desktop-layout) in Webex Help Center.
For more information on sample custom widgets, see https://github.com/CiscoDevNet/webex-contact-center-widget-starter/tree/master/Examples.

### iFrame Widgets

The iFrame widget is a special widget that can be used to embed a different application. The iFrame widget creates an HTML iFrame and renders your application. The Content Security Policy (CSP) headers are required in the iFrame widget URL's response headers. To enable CSP headers for your application that you are embedding, see [Content Security Policy (CSP)](https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP) and [CSP: frame-ancestors](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/frame-ancestors). Allow only the exact HTTPS origin of each approved Desktop deployment in `frame-ancestors`. Replace the example origin below with the origin for your deployment; list additional approved origins explicitly.

**Example**

```http
Content-Security-Policy: frame-ancestors https://desktop.wxcc-us1.cisco.com;
```

**Note:** If the `setTimeout` and `setInterval` methods are used in developing a widget, consider the recent Google Chrome throttling impact. For more information, see https://developer.chrome.com/blog/timer-throttling-in-chrome-88/.

The `Web Workers` API can be used to run timers with a chain count of more than five, and each count is less than a minute. For more information, see https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API/Using_web_workers.

## Get Started

We suggest to have a setup in which you are able to place your widget in a larger Desktop environment. For reference, you can use one of our boilerplate projects available at the Cisco DevNet Git Hub community: https://github.com/CiscoDevNet/webex-contact-center-widget-starter.

Alternatively, we suggest you to have a sandbox environment where you are able to place your widget (Web Component) in a constrained container and have an opportunity to test the following:

- Responsive behavior for various container sizes (from preferred to full screen).

  **Note:** Responsive web components make your webpage visually appealing on all devices and are easy to use. You must use responsive iFrame widgets. For more information, see [Create custom desktop layout](https://help.webex.com/en-us/article/ng08gqeb/Create-custom-desktop-layout) in Webex Help Center.

- Overflow behavior on how your widget appears and behaves when its contents overflow on either X or Y axis (that is, scrollbars).

- Reacting to data passed into the widget. For more information about reactive component practices, see [Reactive Property or Attribute Change](https://developer.webex.com/docs/desktop-custom-widgets#reactive-property-or-attribute-change).

- Light or Dark mode support (if you are using our Momentum UI Web Component library).

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

## Momentum UI Web Component Library

We encourage you to explore our UI component library to enable you to build a custom widget interface faster with the Webex Contact Center Desktop visual language. For more information on the momentum UI Web Component library, see [GitHub](https://github.com/momentum-design/momentum-ui/tree/master/web-components) and [MIT](https://github.com/momentum-design/momentum-ui/blob/master/LICENSE) license. If you encounter any issues, report them on our [GitHub](https://github.com/momentum-design/momentum-ui/issues) page.

The current collection includes:

- Activity Button
- Alert
- Alert Banner
- Avatar
- Badge
- Breadcrumbs
- Button
- Checkbox
- Editable Field
- Floating Modal
- Help Text
- Icon
- Input
- Label
- Link
- List
- List Item
- Loading indicator
- Meeting Alert
- Menu Overlay
- Modal
- Phone Number Input
- Progress Bar
- Radio
- Spinner
- Table
- Tabs
- Task Item
- Theme
- Toggle Switch
- Tooltip

Momentum UI Web Component library will continue to grow and improve over time. We welcome any contributions. For more information on the Web Components library, see [Components](https://momentum.design/components/overview).

**Figure 2. Sample Components on Desktop**

![sample components on agent desktop](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt638ead59dbbfba5a/69b1e95f2871456212940541/agentx_sample_components_279555997a.jpeg)

### Light or Dark Mode Support

In Webex Contact Center Desktop, we support Light and Dark mode by default. This is achieved through Momentum UI Web Component `<md-theme>`. When wrapped around components, `<md-theme>` assigns values to a collection of predefined core CSS color variables and [custom CSS properties](https://developer.mozilla.org/en-US/docs/Web/CSS/--*). These properties switch from light to dark on a theme switch. The advantage of relying on CSS custom properties is that they pierce Shadow DOM and can be used inside many nested layers of Shadow DOM.

**Note:** You can use the core CSS color variables if your widget CSS is in the following format:

```css
.container {
  background-color: var(--md-primary-bg-color, #fff);
}
```

The following Sass examples reproduce theme values for a custom element. Install `@momentum-ui/core`; its `scss/colors/settings-base.scss` exports the `$md-*` color tokens used here. Configure your Sass compiler to resolve packages from `node_modules`. The selectors use a `dark-mode` attribute on your custom element. Bind the Desktop theme to your widget’s `darkMode` property in the layout, then reflect that Boolean property to the attribute whenever Desktop updates it: 
```json
{
  "widgets": {
    "themed-widget": {
      "comp": "themed-widget",
      "properties": { "darkMode": "$STORE.app.darkMode" }
    }
  }
}
```

Implement the property in your Web Component (merge this setter into the class that owns your widget):

```javascript
class ThemedWidget extends HTMLElement {
  set darkMode(value) {
    if (typeof value === "boolean") {
      this.setAttribute("dark-mode", String(value));
    } else {
      this.removeAttribute("dark-mode");
    }
  }
}
```

The Sass below belongs to the widget’s Shadow DOM stylesheet. With `dark-mode="false"`, only the light selector matches; with `dark-mode="true"`, only the dark selector matches. If the attribute is missing, neither override applies and Desktop’s CSS variables remain inherited. Widgets that only consume Desktop theme colors should use `var(--md-...)` as above.


**Example: Light and Dark Mode**

```scss
@use "@momentum-ui/core/scss/colors/settings-base" as *;

:host([dark-mode="false"]) {
  --md-default-focus-outline-color: #{$md-blue-60};

  --md-primary-bg-color: #{$md-white};
  --md-secondary-bg-color: #{$md-gray-05};
  --md-secondary-white-bg-color: #{$md-white};
  --md-tertiary-bg-color: #{$md-gray-10};
  --md-tertiary-white-bg-color: #{$md-white};
  --md-quaternary-bg-color: #{$md-gray-20};

  --md-primary-success-bg-color: #{$md-green-10};
  --md-primary-success-text-color: #{$md-green-70};

  --md-primary-text-color: #{$md-gray-100};
  --md-secondary-text-color: #{$md-gray-70};
  --md-disabled-text-color: #{$md-gray-40};
  --md-highlight-text-color: #{$md-theme-20};
  --md-hyperlink-text-color: #{$md-theme-70};
  --md-hyperlink-hover-text-color: #{$md-theme-90};
  --md-hyperlink-focus-text-color: #{$md-theme-70};

  --md-primary-seperator-color: #{$md-gray-30};
  --md-secondary-seperator-color: #{$md-gray-40};

  --md-presence-active-bg-color: #{$md-green-50};
  --md-presence-do-not-disturb-bg-color: #{$md-red-60};
  --md-presence-away-bg-color: #{$md-gray-30};
  --md-presence-busy-bg-color: #{$md-yellow-40};
}

:host([dark-mode="true"]) {
  --md-default-focus-outline-color: #{$md-blue-40};

  --md-primary-bg-color: #{$md-gray-100};
  --md-secondary-bg-color: #{$md-gray-95};
  --md-secondary-white-bg-color: #{$md-gray-95};
  --md-tertiary-bg-color: #{$md-gray-90};
  --md-tertiary-white-bg-color: #{$md-gray-90};
  --md-quaternary-bg-color: #{$md-gray-80};

  --md-primary-success-bg-color: #{$md-mint-70};
  --md-primary-success-text-color: #{$md-mint-20};

  --md-primary-text-color: #{$md-gray-05};
  --md-secondary-text-color: #{$md-gray-40};
  --md-disabled-text-color: #{$md-gray-70};
  --md-highlight-text-color: #{$md-theme-80};
  --md-hyperlink-text-color: #{$md-theme-40};
  --md-hyperlink-hover-text-color: #{$md-theme-20};
  --md-hyperlink-focus-text-color: #{$md-theme-40};

  --md-primary-seperator-color: #{$md-gray-70};
  --md-secondary-seperator-color: #{$md-gray-60};

  --md-presence-active-bg-color: #{$md-green-50};
  --md-presence-do-not-disturb-bg-color: #{$md-red-60};
  --md-presence-away-bg-color: #{$md-gray-30};
  --md-presence-busy-bg-color: #{$md-yellow-40};

  --md-auto-wrapup-bg-color: #{$md-blue-90};
}
```

## Activities

### IdleInActivityTracker

The `idleInActivityTracker` method tracks every interaction of a user with the Desktop. The
administrator configures the Desktop inactivity timeout value. If the agent is inactive on the Desktop for a specified duration, the agent is notified with the <b>Prolonged Inactivity</b> dialog box. The dialog
box is displayed one minute before the configured timeout occurs, and the agent must take action before the
timer runs out.
The `iFrame` windows are isolated from the parent window. To track any user events inside a widget that is
rendered within an iFrame, use the `postMessage()` method.
To handle inactivity timer inside an iFrame:

1. Ensure that your widget or application is running inside an iFrame.
2. Register an event listener for the eventTypes `click`, `wheel`, and `keydown`.
3. Use the `postMessage()` method to communicate the eventTypes to the Desktop (parent window) on
   `wxcc-desktop-iframe-widget-event`.

Add the following code to the main JavaScript file of an iframe widget. Replace `desktopOrigin` with the exact origin of the parent Desktop deployment:

```javascript
// Use the exact HTTPS origin of your Desktop deployment.
const desktopOrigin = "https://desktop.wxcc-us1.cisco.com";
const eventTypes = ["click", "wheel", "keydown"];

function reportActivity(userEvent) {
  window.parent.postMessage({
    key: "wxcc-desktop-iframe-widget-event",
    type: userEvent.type
  }, desktopOrigin);
}

if (window.self !== window.top) {
  for (const eventType of eventTypes) {
    window.addEventListener(eventType, reportActivity);
  }
}

// Call this when the widget is disposed.
function cleanupActivityTracker() {
  for (const eventType of eventTypes) {
    window.removeEventListener(eventType, reportActivity);
  }
}
```

## Related Pages

- [Agent Desktop overview](https://developer.webex.com/docs/desktop)
- [Desktop SDK Reference](https://developer.webex.com/docs/desktop-sdk-reference)
