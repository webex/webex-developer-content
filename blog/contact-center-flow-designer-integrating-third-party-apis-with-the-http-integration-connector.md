---
type: Article
title: 'Contact Center Flow Designer: Integrating Third-Party APIs with the HTTP Integration Connector'
canonical_url: https://developer.webex.com/blog/contact-center-flow-designer-integrating-third-party-apis-with-the-http-integration-connector
content_type: blog
date: '2024-05-13'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/contact-center-flow-designer-integrating-third-party-apis-with-the-http-integration-connector)

There is a lot going on under the hood of most contact center technology stacks during day-to-day operations. A contact center agent serves hundreds of customers daily and handles a lot of sensitive data. A customer’s time and experience are extremely valuable and can make or break potential revenue for any organization. Though speaking to a representative is still the top preferred engagement channel for customers, there are still ways that developers can build applications and services that make digital-first experiences. These experiences can build the confidence of an agent to handle sensitive data, are comfortable for agents to use, and can streamline the “Zero to Hello Agent” time for customers with important support needs. The Webex Contact Center Flow Designer is an integration surface that provides development teams with the tools necessary to plug in third-party APIs for congruent technologies to run alongside Webex Contact Center call handling and routing strategy software.

### Pre-requisites For Setting Up a Flow Designer Connector

Best practices ask a developer’s third-party API to either be set up with a path for an integration to be registered To ensure a smooth integration process within the Flow Designer, it is recommended that developers prepare their third-party API to support one of two authentication methods:

- **OAuth Authentication**: Ideally, the third-party API should have a dedicated endpoint that allows for the registration of the integration on your platform. This endpoint should facilitate an OAuth authentication flow, enabling users to securely connect their third-party services with the Webex Contact Center.
- **Basic Authentication**: Alternatively, the API can provide a Basic Authentication method, which requires a username and password for access.

Once the third-party API is ready to support one of these authentication methods, the Webex Contact Center Administrator can then proceed to configure the integration connector by following the provided setup instructions. This involves accessing the necessary authorization credentials and applying them within the Flow Designer to establish the connection.

### Setting Up Third-Party API Custom Connectors in Control Hub

To set up a third-party connector in Control Hub:

1. An organization administrator should log into Control Hub at [https://admin.webex.com](https://admin.webex.com/).
1. Navigate to **Services** &gt; **Contact Center** &gt; **Tenant Settings** &gt; **Integrations** &gt; **Connectors**.
1. On the Custom Connectors Card click Set Up or Add more
1. In the **Name** field, enter a relevant name for the connector that a user can associate with the service when discovered in the Flow Designer HTTPS node setup.
1. Choose an authentication type from the **Authentication Type** drop-down (**OAuth** or **Basic Auth**).
1. In the **Resource Domain URL** field, enter the URL of the third-party service API (HTTPS Required).
1. If your API uses OAuth 2.0, choose either **Client Credentials** or **Password Grant Types**:
    1. In the **Client ID** field, enter the third-party API service client ID issued for the integration.
    1. In the **Client Secret field**, enter the Client Secret.
    1. In the **Token URL** field, enter the token URL of the authorization server.
    1. In the **Scope** field, enter the scope for the client credentials grant.
1. If your API uses basic auth and the grant type is password grant:
    1. In the **Username** field, enter the username of the service account.
    1. In the **Password** field, enter the password of the service account.
    1. In the **Validation URL** field, enter the URL to validate the username and password.
1. Click **Done** &gt; **Close**.

<br/>

### Discovering The Connector in the Webex Contact Center Flow Designer

Now that the connector is set up, Webex Contact Center customers can leverage your software from the Flow designer.

To access the connector in your sandbox org:

1. Login to the Webex Control Hub at [https://admin.webex.com/login](https://admin.webex.com/login).
1. Go to **Service** &gt; **Contact Center** &gt; **Customer Experience** &gt; **Flows** and either select an existing flow or create a new flow.
    

> **Info**
>
> When in the Flow Designer application make sure that the **Edit** option is toggled on.


1. From the **Activity Library** in the left navigation pane, select an HTTP request node from the **Flow Control** section of the options.
1. Click on the node in the Flow Builder, and under **HTTP Request Settings**, toggle on **Use Authenticated Endpoint**.
1. On the **Connector** drop-down, the custom connector you just created should be available to use:

    ![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltd01b7cd05e9cbd2d/flow-designer-apis---blog-2.png)

### Need Some Help? We Got You Covered!

We are excited to provide you with support for these features. If you need help, the [Webex Developer Support Team](https://developer.webex.com/support) is standing by and happy to assist. You can also start or join a conversation on the [Webex for Developers Community Forum](https://cs.co/WebexDeveloperCommunity).
