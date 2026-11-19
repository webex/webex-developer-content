---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-quickstart
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Import the Meetings SDK
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-quickstart). [Full Markdown](../../../../../docs/sdks/webex-meetings-sdk-web-quickstart.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Welcome to the Quick Start Guide for the Webex Meetings SDK. This guide is designed to provide developers with a concise walkthrough to swiftly set up, authorize, and test the core meeting functionalities within the Meeting SDK. 

---

By following the sequential flow of this document and integrating the provided code snippets, you'll be able to authenticate your application and create and manage your first meetings. Whether you're new to Webex's Meeting SDK or looking to brush up on the basics, this guide ensures a streamlined experience to get you up and running in no time. Let's dive in!

## Selected section

## Import the Meetings SDK

To install the latest stable version of the Meetings SDK use either NPM or CDN.

### NPM



> **Info**
>
> We test against the [Active LTS](https://github.com/nodejs/Release#release-schedule) (Long Term Support) version of Node.js and use `npm@6` to run [security audits](https://docs.npmjs.com/getting-started/running-a-security-audit).



The Meetings SDK is available as a `nodejs` module via NPM. You can install it using either `yarn` or `npm` utilities:

```bash
 yarn add webex
```

or

```bash
npm install webex
```

### CDN

A minified version of the Meeting SDK is also provided via the [unpkg](https://unpkg.com/) or [jsdelivr](https://jsdelivr.com/) Content Delivery Networks (CDN). To include the CDN Meeting SDK:

```html
 <!-- unpkg -->
 <script crossorigin src="https://unpkg.com/webex/umd/webex.min.js"></script>
 <!-- jsdelivr -->
 <script crossorigin src="https://cdn.jsdelivr.net/npm/webex/umd/webex.min.js"></script>
```

If you're already using a bundler like [Webpack](https://webpack.js.org/) or [Rollup](https://rollupjs.org/)) you can simply import or require the package and use the above snippet, assigning the initialized `webex` variable to `window.webex`.

We also provide a `meetings` specific SDK via [unpkg](https://unpkg.com/). Access by including the following code:

```html
 <script crossorigin src="https://unpkg.com/webex/umd/meetings.min.js"></script>
```
