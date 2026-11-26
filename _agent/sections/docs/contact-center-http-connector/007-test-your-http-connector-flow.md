---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-center-http-connector
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Test Your HTTP Connector Flow
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-center-http-connector). [Full Markdown](../../../../docs/contact-center-http-connector.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites](002-prerequisites.md)

## Article introduction

---

This article provides a comprehensive guide to customizing routing workflows by using the Webex Contact Center HTTP Connector to call Webex Contact Center APIs. It covers a variety of essential topics, including the steps to create a native HTTP connector, configure HTTP request activities, execute GraphQL queries, and best practices for optimal use. By providing practical use cases and detailed instructions, this guide aims to empower flow developers to leverage the powerful capabilities of the Webex Contact Center Flow Designer for seamless API integration and custom logic orchestration.

## Selected section

## Test Your HTTP Connector Flow

To test your new HTTP Connector flow you can either play the variables content via Text To Speech or use the Debug mode:

1. Make sure you’ve saved and published your flow.
1. Select the **Debug** tab in the Flow Designer.
1. Call in to the entry point number associated with the flow, and scroll down to the HTTP Request activity to see the response:
    ![Image described in surrounding text.](https://s3.amazonaws.com/devportal.cms.devus1/webex_contact_center_http_connector_20_4093ba4141.png)

**Note:** The Debug tab marks the execution of the HTTP activity as successful but does not provide the actual HTTP response code. For example, if the response code is returned as 500, the activity execution will still be marked as “success”.

**Note:** This debugging method is to be applied **ONLY** why creating and debugging the HTTP activity. Do not log responses by assigning a response body to a flow variable in a production application!
