---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-sdk-getting-started
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Get Started
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/desktop-sdk-getting-started). [Full Markdown](../../../../docs/desktop-sdk-getting-started.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Install and initialize the Desktop SDK to access Desktop modules from custom widgets.

## Selected section

## Get Started

To start using the JavaScript SDK, you can use any of the following options:

- Run the following command in your project folder: `npm install @wxcc-desktop/sdk --save` or `yarn add @wxcc-desktop/sdk`
- Alternatively, add the following entry to your package.json file:

```json
{
"dependencies": {
    "@wxcc-desktop/sdk": "^3.0.1"
}
}
```

- If you also choose to use our Momentum-ui Web Component library, you must add:

```json
{
"peerDependencies": {
    "@momentum-ui/core": "19.9.2",
    "@momentum-ui/icons": "7.45.0",
    "@momentum-ui/utils": "6.2.7",
    "@momentum-ui/web-components": "^2.0.13",
    "lit-element": "^2.3.1",
    "lit-html": "^1.2.1"
}
}
```

In addition, to access the type definition of return Promise for the JavaScript SDK requests, install the following package:

```json
{
"devDependencies": {
    "@wxcc-desktop/sdk-types": "^1.0.2"
}
}
```

**Note:** Momentum and lit-element dependencies are added to `peerDependencies`. These dependencies are present in Desktop, and should not be imported twice. There is no way to maintain the same versions in your widget and in Desktop.

Once you have installed the package in your project, include it in the appropriate component file following the ES6 import pattern: `import {Desktop} from "@wxcc-desktop/sdk";`
