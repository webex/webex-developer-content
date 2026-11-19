---
type: Guide
title: Contact Center HTTP Connector
display_title: Contact Center HTTP Connector
canonical_url: https://developer.webex.com/docs/contact-center-http-connector
content_type: documentation
product_group:
- webex-contact-center
categories:
- webex-contact-center
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/contact-center-http-connector)

---

This article provides a comprehensive guide to customizing routing workflows by using the Webex Contact Center HTTP Connector to call Webex Contact Center APIs. It covers a variety of essential topics, including the steps to create a native HTTP connector, configure HTTP request activities, execute GraphQL queries, and best practices for optimal use. By providing practical use cases and detailed instructions, this guide aims to empower flow developers to leverage the powerful capabilities of the Webex Contact Center Flow Designer for seamless API integration and custom logic orchestration.

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

## Prerequisites

Before continuing, make sure you meet the following prerequisites:

- A Webex Contact Center organization on FLEX3 licenses.

In addition, the user setting up the connector should have one of these three roles:

- Full Administrator
- External Full Administrator
- Contact Center Service Administrator

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

## Test Your HTTP Connector Flow

To test your new HTTP Connector flow you can either play the variables content via Text To Speech or use the Debug mode:

1. Make sure you’ve saved and published your flow.
1. Select the **Debug** tab in the Flow Designer.
1. Call in to the entry point number associated with the flow, and scroll down to the HTTP Request activity to see the response:
    ![Image described in surrounding text.](https://s3.amazonaws.com/devportal.cms.devus1/webex_contact_center_http_connector_20_4093ba4141.png)

**Note:** The Debug tab marks the execution of the HTTP activity as successful but does not provide the actual HTTP response code. For example, if the response code is returned as 500, the activity execution will still be marked as “success”.

**Note:** This debugging method is to be applied **ONLY** why creating and debugging the HTTP activity. Do not log responses by assigning a response body to a flow variable in a production application!

## Best Practices for using the HTTP Connector

When working with the HTTP Connector, keep the following points in mind:

- Always ensure that no sensitive response is stored in the flow logs. The flow designer encrypts the request and response body to ensure that no sensitive information is stored in the logs.
- The HTTP Connector is rate limited. All API calls originating from flow designer are rate limited based on the anticipated load. While we hope to service all requests, you may encounter `429 Too many requests`.
- Ensure that **ALL** error codes are handled using a **Case Activity** for the error codes listed in the API definition. You can find the output variable, `HTTP_Request.httpStatusCode`, in the variable dropdown list.
    ![Image described in surrounding text.](https://s3.amazonaws.com/devportal.cms.devus1/webex_contact_center_http_connector_21_e41abb79b8.png)
- Learn more about common API errors here: ([/docs/common-api-errors](https://developer.webex.com/docs/common-api-errors)).
- You can optimize your flows by creating subflows with the **HTTP Activity** and **Case/Condition Activity** to ensure that all error cases are handled.
- If the API takes more than one second to execute, you can play music on wait by navigating to global settings in the right-hand panel.
