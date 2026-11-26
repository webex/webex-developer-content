---
type: Excerpt
canonical_url: https://developer.webex.com/docs/cc-web-widgets-quickstart
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Update the package.json File
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/cc-web-widgets-quickstart). [Full Markdown](../../../../docs/cc-web-widgets-quickstart.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites](001-prerequisites.md) [Known Issues/Limitations](010-known-issues-limitations.md)

## Article introduction

This Quickstart Guide walks you through integrating Webex Contact Center capabilities using React widgets into your application from the ground up. Follow these steps to create a fully functional application.

## Selected section

## Update the package.json File

```json
{
  "name": "My CC Project",
  "version": "1.0.0",
  "scripts": {
    "start": "webpack serve",
    "build": "webpack --mode production"
  },
  "dependencies": {
    "@momentum-ui/react-collaboration": "26.201.9",
    "@webex/cc-widgets": "1.28.0-next.3",
    "react": "18.3.1",
    "react-dom": "18.3.1"
  },
  "devDependencies": {
    "@babel/core": "7.28.5",
    "@babel/preset-env": "7.28.5",
    "@babel/preset-react": "7.28.5",
    "babel-loader": "10.0.0",
    "css-loader": "7.1.2",
    "html-webpack-plugin": "5.6.5",
    "husky": "9.1.7",
    "sass": "1.94.2",
    "sass-loader": "16.0.6",
    "style-loader": "4.0.0",
    "webpack": "5.103.0",
    "webpack-cli": "6.0.1",
    "webpack-dev-server": "5.2.2"
  }
}
```

**Note**:

1. For bundlers other than webpack, install and configure the dependencies accordingly.
2. Adding `husky` is only required when using npm instead of yarn. Use `npm install --ignore-scripts` if you remove it from the `package.json` file.

Add the following to the `package.json` if you are using `yarn`:

```json
"resolutions": {
  "@momentum-design/components": "0.53.8",
  "@momentum-design/icons": "0.17.0",
  "@momentum-design/brand-visuals": "0.10.0"
}
```

Add the following to the `package.json` if you are using `npm`:

```json
"overrides": {
  "@momentum-design/components": "0.53.8",
  "@momentum-design/icons": "0.17.0",
  "@momentum-design/brand-visuals": "0.10.0"
}
```
