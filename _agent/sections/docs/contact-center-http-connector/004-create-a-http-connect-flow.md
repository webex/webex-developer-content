---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-center-http-connector
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Create a HTTP Connect Flow
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-center-http-connector). [Full Markdown](../../../../docs/contact-center-http-connector.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites](002-prerequisites.md)

## Article introduction

---

This article provides a comprehensive guide to customizing routing workflows by using the Webex Contact Center HTTP Connector to call Webex Contact Center APIs. It covers a variety of essential topics, including the steps to create a native HTTP connector, configure HTTP request activities, execute GraphQL queries, and best practices for optimal use. By providing practical use cases and detailed instructions, this guide aims to empower flow developers to leverage the powerful capabilities of the Webex Contact Center Flow Designer for seamless API integration and custom logic orchestration.

## Selected section

## Create a HTTP Connect Flow

With the connector created, you’ll create a new flow using the Contact Center Flow Designer.

To create a new flow:

1. If you’re not already in **Contact Center** in [Webex Control Hub](https://admin.webex.com/), navigate to **Contact Center** and then select **Flows** in the left-hand nav. Choose **Manage Flows** and select **Create Flows** from the drop-down menu:
    ![Image described in surrounding text.](https://s3.amazonaws.com/devportal.cms.devus1/webex_contact_center_http_connector_5_abe41b0af6.png)
1. Enter a unique alphanumeric flow name and select **Start Building Flow**:
    ![Image described in surrounding text.](https://s3.amazonaws.com/devportal.cms.devus1/webex_contact_center_http_connector_6_d5192a6411.png)
1. Once the flow canvas loads, find the **HTTP Request** activity in the left-hand palette, and drag and drop it onto the canvas:
    ![Image described in surrounding text.](https://s3.amazonaws.com/devportal.cms.devus1/webex_contact_center_http_connector_7_0d2d147c51.png)
1. Next, select the connection node on the right-hand side of the **Start Flow** activity and drag it to the left-hand connection node on the left side of your new **HTTP Request** activity to create a flow connection:
    ![Image described in surrounding text.](https://s3.amazonaws.com/devportal.cms.devus1/webex_contact_center_http_connector_8_8c1186eaf2.png)
1. Select the **HTTP Request** activity and fill in the required information in the right-hand panel as described in the next section.
