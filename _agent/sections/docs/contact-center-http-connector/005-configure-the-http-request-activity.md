---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-center-http-connector
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Configure the HTTP Request Activity
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-center-http-connector). [Full Markdown](../../../../docs/contact-center-http-connector.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites](002-prerequisites.md)

## Article introduction

---

This article provides a comprehensive guide to customizing routing workflows by using the Webex Contact Center HTTP Connector to call Webex Contact Center APIs. It covers a variety of essential topics, including the steps to create a native HTTP connector, configure HTTP request activities, execute GraphQL queries, and best practices for optimal use. By providing practical use cases and detailed instructions, this guide aims to empower flow developers to leverage the powerful capabilities of the Webex Contact Center Flow Designer for seamless API integration and custom logic orchestration.

## Selected section

## Configure the HTTP Request Activity

When the **HTTP Request** activity is placed on the right-hand panel, you’ll need to add the necessary values to make an outbound API call.

To determine the required values:

1. Navigate to the [Webex Contact Center Developer Portal](https://developer.webex.com/docs/getting-started/) documentation site and login using your org administrator credentials.
1. From the **API REFERENCE** section in the left hand nav, choose the API you want to use for your HTTP request.
1. Gather the following information from the REST endpoint you’d like to use. In this example, we’re using the **List Global Variables** endpoint from the **Global Variables** API:
    ![Image described in surrounding text.](https://s3.amazonaws.com/devportal.cms.devus1/webex_contact_center_http_connector_9_b0c28c0730.png)
    1. The verb for the REST endpoint. In this case it’s `GET`.
    1. The request path for the endpoint. In this case it’s `/organization/{orgid}/v2/cad-variable`
    1. The `orgid` for your organization. Select Try Out and copy this from the orgid field in the Parameters section. You’ll add this in place of the `{orgid}` placeholder in the request path: `/organization/3fa96685-e81e-468a-b70b-84111ec0b127/v2/cad-variable` which is the value you’ll use in the HTTP Request activity.
    1. Any query parameters you’d like to use in the request. In this case, for example, `page`, `pageSize`, `filter`, etc.
1. Navigate back to Flow Designer and select the **HTTP Request** activity:
    ![Image described in surrounding text.](https://s3.amazonaws.com/devportal.cms.devus1/webex_contact_center_http_connector_10_ad79e3da87.png)
1. Fill in the **HTTP Request** activity’s form using the information you’ve gathered above:
    ![Image described in surrounding text.](https://s3.amazonaws.com/devportal.cms.devus1/webex_contact_center_http_connector_11_b74b19e3dc.png)
    Use Authenticated Endpoint: Make sure to toggle this checkbox on for all CC API access.
    1. **Connector**: Select the connector you created above from the drop-down list.
    1. **Request Path**: Use the request path from the REST endpoint you selected above.
    1. **Method**: Choose the REST verb for the REST endpoint you selected above.
    1. **Query Parameters**: Add any query parameters you’d like to use from the REST endpoint you selected above.
    1. **Content Type**: Select `Application/JSON` from the drop-down list.
    1. **Parse Settings:** Get your HTTP response and save it to a variable by creating a flow variable (click on the canvas to create one). Use a [JSON Path](https://jsonpath.com/) expression to find specific fields as needed. You can use the PlayMessage flow activity to play them back.

    ![Image described in surrounding text.](https://s3.amazonaws.com/devportal.cms.devus1/webex_contact_center_http_connector_12_7dfe37fb13.png)

1. Drag an **End Flow** activity from the activity library to the flow canvas and connect it to the right-hand node of the **HTTP Request** activity.
    ![Image described in surrounding text.](https://s3.amazonaws.com/devportal.cms.devus1/webex_contact_center_http_connector_13_6e79c13f86.png)
1. Set the **Validation** toggle at the bottom right to On and select **Publish Flow.**
    ![Image described in surrounding text.](https://s3.amazonaws.com/devportal.cms.devus1/webex_contact_center_http_connector_14_d1e7c14059.png)
1. Continue to **Test Your HTTP Connect Flow** below.
