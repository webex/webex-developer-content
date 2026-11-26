---
type: Excerpt
canonical_url: https://developer.webex.com/docs/widgets-callcontrolcad-webex-better-together-widgets-beta
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Install the beta Widgets package
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/widgets-callcontrolcad-webex-better-together-widgets-beta). [Full Markdown](../../../../docs/widgets-callcontrolcad-webex-better-together-widgets-beta.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md) [Release scope and limitations](006-release-scope-and-limitations.md)

## Article introduction

Use this guide to test Webex Better Together with the Webex Contact Center Widgets package. Agents can handle supported voice-call actions from an embedded host application while the call runs in Webex App on the same computer.

## Selected section

## Install the beta Widgets package

Use `@webex/cc-widgets` version `1.28.0-next.60` or later from this beta train. For a widgets-only host, install the Widgets package; use a matching SDK and Widgets release set when managing both dependencies directly.

```bash
npm install @webex/cc-widgets@1.28.0-next.60
```

Or with Yarn:

```bash
yarn add @webex/cc-widgets@1.28.0-next.60
```
