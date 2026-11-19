---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-custom-widgets
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Momentum UI Web Component Library
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/desktop-custom-widgets). [Full Markdown](../../../../docs/desktop-custom-widgets.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Build and test Web Components and iframe widgets for Webex Contact Center Desktop.

## Selected section

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
