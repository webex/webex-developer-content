---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-better-together-sdk-beta
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Install the beta SDK
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-better-together-sdk-beta). [Full Markdown](../../../../../docs/sdks/webex-better-together-sdk-beta.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Overview and limitations](001-overview-and-limitations.md) [Before you begin](002-before-you-begin.md)

## Article introduction

Use this guide to integrate and test Webex Better Together with the Webex Contact Center SDK. It lets an agent use a host application for call controls while the voice call runs in Webex App on the same computer.

## Selected section

## Install the beta SDK

Use `@webex/contact-center@3.12.0-next.131` for this beta guide. Pin the package version so an unpinned install does not select a different build.

```bash
npm install @webex/contact-center@3.12.0-next.131
```

Or with Yarn:

```bash
yarn add @webex/contact-center@3.12.0-next.131
```
