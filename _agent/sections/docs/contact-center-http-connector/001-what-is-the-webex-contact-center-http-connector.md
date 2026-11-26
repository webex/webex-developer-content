---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-center-http-connector
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- What is the Webex Contact Center HTTP Connector?
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-center-http-connector). [Full Markdown](../../../../docs/contact-center-http-connector.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites](002-prerequisites.md)

## Article introduction

---

This article provides a comprehensive guide to customizing routing workflows by using the Webex Contact Center HTTP Connector to call Webex Contact Center APIs. It covers a variety of essential topics, including the steps to create a native HTTP connector, configure HTTP request activities, execute GraphQL queries, and best practices for optimal use. By providing practical use cases and detailed instructions, this guide aims to empower flow developers to leverage the powerful capabilities of the Webex Contact Center Flow Designer for seamless API integration and custom logic orchestration.

## Selected section

## What is the Webex Contact Center HTTP Connector?

Previously, developers were required to maintain their own access tokens and refresh logic for invoking Webex CC APIs from the flow designer, now the native HTTP connector will manage the tokens behind the scenes. Flow developers can simply browse through the APIs on the developer portal and invoke them from the HTTP activity on the flow designer.

Connectors in Contact Center are an entity on Control Hub that enables an organization to make API calls from the flow designer. To make an API call, the following elements are required:

- Resource Domain (internally managed)
- Credentials (internally managed)
- API path
- Request Headers
- Request Body

The following diagram describes the HTTP connector flow:

![Image described in surrounding text.](https://s3.amazonaws.com/devportal.cms.devus1/webex_contact_center_http_connector_1_486322320c.png)

### Use Cases

The Webex Contact Center HTTP Connector can enhance your contact center workflows in several real-world scenarios. It allows for real-time customer data retrieval and support dynamic routing based on internal data. For example:

- **Admin Workflows:** Specific workflows can be established to allow administrators to make configuration changes, such as updating a menu or modifying business hours.
- **Preferred Agent Routing/Last Agent Routing:** Callers can specify their preferred agent, and the APIs can route the call to that particular agent.
- **Journey Data-Based Call Routing:** Caller information is stored as part of [Journey Data Services](https://developer.webex.com/docs/journey-getting-started). The [JDS APIs](https://developer.webex.com/docs/api/v1/journey-data) can be used to store caller information or perform data lookups.
- **CSAT/Rating-Based Routing:** Routing logic can be customized based on the CSAT information of agents in a specific queue for premium customers.
- **Least Handle Time Agent-Based Routing:** Routing logic can be configured to direct calls to the agent with the least handle time for quick inquiries or premium customers.
- **Least Wait Time Queue-Based Routing:** Call flows can be directed to the queues with the shortest wait times.
- **Least Handle Time Queue-Based Routing:** Routing logic can be set up to direct calls to the queues with the least handle time.
- **Externalizing Post-Call Data:** Call-related information or metadata can be sent to an external system using the HTTP Activity in the event flow.
