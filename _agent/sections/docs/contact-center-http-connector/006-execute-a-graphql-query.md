---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-center-http-connector
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Execute a GraphQL Query
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-center-http-connector). [Full Markdown](../../../../docs/contact-center-http-connector.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites](002-prerequisites.md)

## Article introduction

---

This article provides a comprehensive guide to customizing routing workflows by using the Webex Contact Center HTTP Connector to call Webex Contact Center APIs. It covers a variety of essential topics, including the steps to create a native HTTP connector, configure HTTP request activities, execute GraphQL queries, and best practices for optimal use. By providing practical use cases and detailed instructions, this guide aims to empower flow developers to leverage the powerful capabilities of the Webex Contact Center Flow Designer for seamless API integration and custom logic orchestration.

## Selected section

## Execute a GraphQL Query

In addition to accessing any of the Contact Center REST APIs, you can also execute GraphQL queries.

To configure the HTTP Request activity to execute GraphQL queries:

1. Navigate to the [Search API](https://developer.webex.com/docs/api/v1/search) page in the Contact Center Developer Portal and choose **Try Out** and then **Maximize Screen** in the right-hand panel:
    ![Image described in surrounding text.](https://s3.amazonaws.com/devportal.cms.devus1/webex_contact_center_http_connector_15_e41ee8936f.png)
1. In the left-hand edit box of the **GraphQL** section, you can create and debug your GraphQL query:
    ![Image described in surrounding text.](https://s3.amazonaws.com/devportal.cms.devus1/webex_contact_center_http_connector_16_dcd1c3a0f1.png)
1. Once your query is working the way you expect, convert it to a JSON string using any [handy web tool](https://transform.tools/json-to-graphql) or AI chat bot. Some tools don’t remove the Graph QL comments (#). Make sure your JSON string doesn’t have those.
    **Note:** You can find a variety of GraphQL examples in our GitHub repo: [https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples](https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples).
1. Referring to the previous section, update the **HTTP Response** activity in your flow with the following values:
    1. **Request Path**: Set to `/search`.
    1. **Method**: Set to `POST`.
    1. **Query Parameters**: Add a query parameter with the key `orgid` and set the value to your organization ID.
    1. **Content Type**: Select `Application/JSON` from the drop-down list.
    1. **Request Body**: Paste in your GraphQL query that you’ve converted to a JSON string. Here is an example showing task IDs: `{ "query": "{ taskDetails ( from: 1719845438000 to: 1727794389000 ) { tasks { id } }}"}`
1. Store the GraphQL response in a variable by selecting the background canvas of your flow to access the **Global Flow Properties**, scroll down to **Variable Definition**, select the **Configuration** tab and choose **Add Flow Variable**:
    ![Image described in surrounding text.](https://s3.amazonaws.com/devportal.cms.devus1/webex_contact_center_http_connector_17_720f627759.png)
1. Enter the following information for the variable and then select **Save**:
    - **Name**: Choose an alphanumeric name for the variable.
    - **Description**: Fill out or leave blank.
    - **Variable Type**: Choose JSON from the drop-down list.
    - **Default Value**: Enter `{}`
    ![Image described in surrounding text.](https://s3.amazonaws.com/devportal.cms.devus1/webex_contact_center_http_connector_18_4f1366b7e1.png)
1. Select the **HTTP Response** activity, scroll down to **Content Type** and choose **JSON** from the drop-down list, select **Output Variable** and choose your newly created variable, and enter `$` in the **Path Expression** edit box:
    ![Image described in surrounding text.](https://s3.amazonaws.com/devportal.cms.devus1/webex_contact_center_http_connector_19_7922cf635a.png)
1. Set the **Validation** toggle at the bottom right to On and select **Publish Flow**:
    ![Image described in surrounding text.](https://s3.amazonaws.com/devportal.cms.devus1/webex_contact_center_http_connector_14_d1e7c14059.png)
1. Continue to **Test Your HTTP Connect Flow** below.
