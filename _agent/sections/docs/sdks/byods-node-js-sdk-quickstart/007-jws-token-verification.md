---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/byods-node-js-sdk-quickstart
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- JWS Token Verification
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/byods-node-js-sdk-quickstart). [Full Markdown](../../../../../docs/sdks/byods-node-js-sdk-quickstart.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites](002-prerequisites.md)

## Article introduction

The Webex Bring Your Own Data Service (BYoDS) Node.js SDK offers a simple way to set up and connect to your data sources when working with Webex services.

---

In this article, we’ll walk you through the steps to get it up and running quickly. For more in-depth details, we encourage you to explore the full documentation on specific features.

## Selected section

## JWS Token Verification

When the `DAS` sends a request to the `DAP`, it includes the `JWS` token in the header. To ensure the request is authentic and not from a malicious source, use the `sdk.verifyJWSToken(jws)` method for easy validation:

```js
const jws = 'a_jws_token';
const response = await sdk.verifyJWSToken(jws);

console.log('Response: ', response);
```
