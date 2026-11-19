---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-localization
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Localization Module
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/desktop-localization). [Full Markdown](../../../../docs/desktop-localization.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before You Begin](001-before-you-begin.md)

## Article introduction

Create and manage localization bundles for lit-element Desktop widgets.

## Selected section

## Localization Module

The `Desktop.i18n` module creates and maintains the localization bundles for lit-element based widgets (in case you considered [Starter Widget](https://github.com/CiscoDevNet/webex-contact-center-widget-starter/tree/master/lit-element) as a base).

The localization module is built based on the [i18next](https://www.i18next.com/) package and enables the widget developer to utilize the Desktop internationalization mechanism and load additional localization bundles to it. For more information on i18next, refer the following resources:

- For `Desktop.i18n` instantiating object, see https://www.i18next.com/overview/api#instance-creation.
- For i18n instance back-end configuration, see https://github.com/i18next/i18next-http-backend.
- For i18n instance languageDetector configuration, see https://github.com/i18next/i18next-browser-languageDetector.
- For i18n instance init options, see https://www.i18next.com/overview/configuration-options.

Using this module implies that your widget has lit-element and lit-html libraries.

```javascript
import {
    Desktop
} from "@wxcc-desktop/sdk";

// CreateOptions are optional.
const i18n = Desktop.i18n.createInstance();
const i18nMixin = Desktop.i18n.createMixin({
    i18n /*Injecting i18n service instance into lit-element mixin */
})

// FYI you can see default options like so
console.log(Desktop.i18n.DEFAULT_INIT_OPTIONS); // => i18n.init options that are using by Desktop by default

// To get started, Init i18n with options to be able call "t" function translations
if (!i18n.isInitialized) {
    // Here, you are adding (merging) your localization package with the Desktop existing set of packages
    const initOptions = Desktop.i18n.getMergedInitOptions(Desktop.i18n.DEFAULT_INIT_OPTIONS || {}, {
        defaultNS: "my-ns", // "ns" here stands for the default JSON file name containing the localization
        ns: ["my-ns"],
        fallbackLng: "en",
        backend: {
            loadPath: "/.../path-to-locales/.../{{lng}}/{{ns}}.json"
        }
    });

    i18n.init(initOptions).catch(err => console.log(err));
}
```

When the service is initialized, create components with the mixin you created earlier:

The mixin subscribes to i18n initialization and language-change events. It requests component updates when initialization completes or the active language changes, and exposes translations through `this.t(...)`.

```typescript
import {
    customElement,
    LitElement
} from "lit-element";
import {
    html
} from "lit-html";

@customElement("my-awesome-component")
export class MyAwesomeComponent extends i18nMixin(LitElement) {
    render() {
        return html`
          <p>${this.t("my-ns:key1")}</p>
          <p>${this.t("my-ns:key2")}</p>
        `;
    }
}
```

### Methods

#### init(initOptions)

Initiates the localization module.

**Example**

```javascript
i18n.init(initOptions);
```

**Parameters**

| Name        | Type   | Description                                                                                            | Required |
| ----------- | ------ | ------------------------------------------------------------------------------------------------------ | -------- |
| initOptions | Object | The init options that are used by Desktop by default. `console.log(Desktop.i18n.DEFAULT_INIT_OPTIONS)` | Yes      |

#### createInstance(createOptions)

Creates the localization bundles for lit-element based widgets.

**Example**

```javascript
const i18n = Desktop.i18n.createInstance();
// returns instance described in https://www.i18next.com/overview/api#instance-creation
```

**Parameters**

| Name          | Type   | Description                                     | Required |
| ------------- | ------ | ----------------------------------------------- | -------- |
| createOptions | Object | Optional configuration for the localization (i18n) instance. Omit it to use the default backend and language detector. | No |
| -->logger | Object | A custom logger implementing `log(...args)`, `warn(...args)`, and `error(...args)`, or a logger returned by `Desktop.logger.createLogger()`. | No |
| -->backend | Object | An i18next backend plugin instance, such as `i18next-http-backend`, used to load localization bundles. | No |
| -->languageDetector | Object | An i18next browser language detector plugin instance, such as `i18next-browser-languagedetector`, used to detect the user's language. | No |

#### createMixin()

Creates the localization (i18n) service instance into lit-element mixing.

**Example**

```javascript
const i18nMixin = Desktop.i18n.createMixin({
  i18n /*Injecting i18n service instance into lit-element mixin */
});
```

#### getMergedInitOptions()

Adds or merges your localization package with the existing set of packages in Desktop.

**Example**

```javascript
const initOptions = Desktop.i18n.getMergedInitOptions(
  Desktop.i18n.DEFAULT_INIT_OPTIONS || {},
  {
    defaultNS: "my-ns", // "ns" here stands for the default JSON file name containing the localization
    ns: ["my-ns"],
    fallbackLng: "en",
    backend: {
      loadPath: "/.../path-to-locales/.../{{lng}}/{{ns}}.json"
    }
  }
);
```

The following table lists the payload details:

| Name                 | Type   | Description                                                                                                                 | Required |
| -------------------- | ------ | --------------------------------------------------------------------------------------------------------------------------- | -------- |
| DEFAULT_INIT_OPTIONS | Object | The init options that are used by Desktop by default.                                                                       | Yes      |
| defaultNS            | String | Default localization JSON file name.                                                                                        | Yes      |
| ns                   | String[] | JSON file name of your locale.                                                                                              | Yes      |
| fallbackLng          | String | Language to use if the file is not found in the configured path or if you cannot provide the preferred language for a user. | Yes      |
| backend              | Object | Contains the load path.                                                                                                     | Yes      |
| -->loadPath          | String | Location of the file path.                                                                                                  | Yes      |

#### cleanup()

Triggers the clean up when init service returns an undefined response.

**Example**

```javascript
class MyWidget {
cleanup() {
    this.SERVICE = undefined;

    this.logger.info("Cleaned");
}
}
```
