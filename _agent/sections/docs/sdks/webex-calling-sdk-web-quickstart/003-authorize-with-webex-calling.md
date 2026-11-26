---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-calling-sdk-web-quickstart
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Authorize with Webex Calling
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-calling-sdk-web-quickstart). [Full Markdown](../../../../../docs/sdks/webex-calling-sdk-web-quickstart.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Welcome to the Quick Start Guide for the Webex Calling SDK. This guide is designed to provide developers with a concise walkthrough to swiftly set up, authorize, and test the core calling functionalities within the Calling SDK.

---

By following the sequential flow of this document and integrating the provided code snippets, you'll be able to authenticate your application and initiate your first calls. Whether you're new to Webex's Calling SDK or looking to brush up on the basics, this guide ensures a streamlined experience to get you up and running in no time. Let's dive in!

## Selected section

## Authorize with Webex Calling

Initiating the authorization process with Webex Calling is the first step to harness the communication capabilities of the SDK. Before diving into call operations, you must first obtain the `Line` object from the `CallingClient`. Once you have the `Line` object in hand, you can invoke the `line.register()` function to create a device, laying the groundwork for initiating and managing voice calls. Before triggering the `register()` method, however, it's crucial to listen for the `registered` event to ensure the device is successfully registered and ready for operations. This section will guide you through these steps.

```javascript
// Get Line object from the callingClient. Currently, only a single
// line is supported in the Calling package

const line = Object.values(callingClient.getLines())[0];

// Listen for the registered event from the line

line.on('registered', (lineInfo) => {
  console.log('Line information: ', lineInfo);
});

line.register();
```
