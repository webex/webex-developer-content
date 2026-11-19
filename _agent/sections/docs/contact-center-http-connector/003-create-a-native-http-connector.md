---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-center-http-connector
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Create a Native HTTP Connector
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-center-http-connector). [Full Markdown](../../../../docs/contact-center-http-connector.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites](002-prerequisites.md)

## Article introduction

---

This article provides a comprehensive guide to customizing routing workflows by using the Webex Contact Center HTTP Connector to call Webex Contact Center APIs. It covers a variety of essential topics, including the steps to create a native HTTP connector, configure HTTP request activities, execute GraphQL queries, and best practices for optimal use. By providing practical use cases and detailed instructions, this guide aims to empower flow developers to leverage the powerful capabilities of the Webex Contact Center Flow Designer for seamless API integration and custom logic orchestration.

## Selected section

## Create a Native HTTP Connector

To create a Webex Contact Center HTTP connector:

1. Login to [Webex Control Hub](https://admin.webex.com/) with your administrator account.
1. Navigate to **Contact Center** in the left hand nav and select **Integrations**, find the card labeled **Webex Contact Center** and select **Set Up**:
    ![Image described in surrounding text.](https://s3.amazonaws.com/devportal.cms.devus1/webex_contact_center_http_connector_2_506b522fec.png)
1. You’ll need to decide the access rights you want for the connector depending on your use case.
    Here are details on the form fields:
    - **Name of the connector:** Used as an identifier in the Flow Designer. Can be any alphanumeric string.
    - **Access:** Define the type of access to grant the tokens for this connector:
        - **Read Only:** Grants the ability to make `GET` API calls with the scopes: `cjp_config``, and ``cjp_config_read.`
        - **Read-Write:** Grants the ability to make `GET`, `POST`, `PUT`, `UPDATE` and `DELETE` API calls with the scopes: `cjp_config``, ``cjp_config_read``, ``cjp_config_write``, and ``cjp_user.`
    - **Authorization:** An admin must authorize this connector and grant permissions for the connector to read, write and modify data in the contact center solution. Select **I authorize** to authorize the connector.
    Select **Add Connector** when you’ve filled out the form:
    ![Image described in surrounding text.](https://s3.amazonaws.com/devportal.cms.devus1/webex_contact_center_http_connector_3_0004ec10b8.png)
1. You’ll receive a success message once the connector is created:
    ![Image described in surrounding text.](https://s3.amazonaws.com/devportal.cms.devus1/webex_contact_center_http_connector_4_7407a8c062.png)
