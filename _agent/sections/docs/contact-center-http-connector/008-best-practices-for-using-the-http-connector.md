---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-center-http-connector
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Best Practices for using the HTTP Connector
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-center-http-connector). [Full Markdown](../../../../docs/contact-center-http-connector.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites](002-prerequisites.md)

## Article introduction

---

This article provides a comprehensive guide to customizing routing workflows by using the Webex Contact Center HTTP Connector to call Webex Contact Center APIs. It covers a variety of essential topics, including the steps to create a native HTTP connector, configure HTTP request activities, execute GraphQL queries, and best practices for optimal use. By providing practical use cases and detailed instructions, this guide aims to empower flow developers to leverage the powerful capabilities of the Webex Contact Center Flow Designer for seamless API integration and custom logic orchestration.

## Selected section

## Best Practices for using the HTTP Connector

When working with the HTTP Connector, keep the following points in mind:

- Always ensure that no sensitive response is stored in the flow logs. The flow designer encrypts the request and response body to ensure that no sensitive information is stored in the logs.
- The HTTP Connector is rate limited. All API calls originating from flow designer are rate limited based on the anticipated load. While we hope to service all requests, you may encounter `429 Too many requests`.
- Ensure that **ALL** error codes are handled using a **Case Activity** for the error codes listed in the API definition. You can find the output variable, `HTTP_Request.httpStatusCode`, in the variable dropdown list.
    ![Image described in surrounding text.](https://s3.amazonaws.com/devportal.cms.devus1/webex_contact_center_http_connector_21_e41abb79b8.png)
- Learn more about common API errors here: ([/docs/common-api-errors](https://developer.webex.com/docs/common-api-errors)).
- You can optimize your flows by creating subflows with the **HTTP Activity** and **Case/Condition Activity** to ensure that all error cases are handled.
- If the API takes more than one second to execute, you can play music on wait by navigating to global settings in the right-hand panel.
