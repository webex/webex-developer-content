---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-custom-widgets
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Build a Custom Widget
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/desktop-custom-widgets). [Full Markdown](../../../../docs/desktop-custom-widgets.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Build and test Web Components and iframe widgets for Webex Contact Center Desktop.

## Selected section

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
