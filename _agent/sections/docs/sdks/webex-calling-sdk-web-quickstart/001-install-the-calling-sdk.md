---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-calling-sdk-web-quickstart
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Install the Calling SDK
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-calling-sdk-web-quickstart). [Full Markdown](../../../../../docs/sdks/webex-calling-sdk-web-quickstart.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Welcome to the Quick Start Guide for the Webex Calling SDK. This guide is designed to provide developers with a concise walkthrough to swiftly set up, authorize, and test the core calling functionalities within the Calling SDK.

---

By following the sequential flow of this document and integrating the provided code snippets, you'll be able to authenticate your application and initiate your first calls. Whether you're new to Webex's Calling SDK or looking to brush up on the basics, this guide ensures a streamlined experience to get you up and running in no time. Let's dive in!

## Selected section

## Install the Calling SDK

To install and consume the latest stable version of the Calling SDK you can use NPM or CDN.

### NPM



> **Info**
>
> We test against the [Active LTS](https://github.com/nodejs/Release#release-schedule) (Long Term Support) version of Node.js and use `npm@6` to run [security audits](https://docs.npmjs.com/getting-started/running-a-security-audit).



The Calling SDK is available in two forms as a `nodejs` module via NPM.
Install either of the following modules based on how you'd like to consume the Calling SDK. For more information on the ways to consume the module, refer to the section below.

* [@webex/calling](https://www.npmjs.com/package/@webex/calling)
* [webex](https://www.npmjs.com/package/webex)

When using the `@webex/calling` package, use these commands to install the package. You'll use these packages for "Option 1" in the section below.
```bash
npm install --save @webex/calling
```
or
```bash
yarn add @webex/calling
```

When using the `webex` package, use these commands to install the package. You'll use this for "Option 2" in the section below.
```bash
npm install --save webex
```
or 
```bash
yarn add webex
```

### CDN

A minified version of the Calling SDK is also provided via the `unpkg.com` Content Delivery Network (CDN). To include the CDN Calling SDK:

```javascript
<script src='https://unpkg.com/webex/umd/calling.min.js'></script>
```
