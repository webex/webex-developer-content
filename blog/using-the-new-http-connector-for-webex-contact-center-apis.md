---
type: Article
title: Using the New HTTP Connector for Webex Contact Center APIs
canonical_url: https://developer.webex.com/blog/using-the-new-http-connector-for-webex-contact-center-apis
content_type: blog
date: '2024-12-10'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/using-the-new-http-connector-for-webex-contact-center-apis)

We are excited to introduce a powerful new feature for Webex Contact Center: the HTTP Connector for Webex Contact Center APIs. This addition empowers organizations to customize their workflows by seamlessly integrating public Webex Contact Center APIs into the Webex Contact Center Flow Designer. With this low-code, no-code platform, flow developers can now easily orchestrate custom logic and enhance their contact center operations.

### What is the Webex Contact Center API Connector?

The Webex Contact Center API Connector is an entity within the Control Hub that allows organizations to make Webex CC API calls directly from the Flow Designer. This feature simplifies the process of invoking public Webex CC APIs by managing tokens natively, enabling developers to focus on building efficient workflows without worrying about the underlying complexities.

In the past, using our Webex Contact Center APIs within Flow Designer required developers to manage tokens manually. This process involved several complex steps: creating an integration for admin login to provide access and refresh tokens, and building a separate token server to store, retrieve, and refresh these tokens. Now, with the introduction of the Webex CC API Connector, all this extra work and setup is no longer necessary! The Webex CC API Connector simplifies the process, allowing seamless integration without the need for additional infrastructure.

In this blog, we are going to highlight one use case for the connector. For a complete walkthrough, be sure to check out the guide at [https://developer.webex.com/webex-contact-center/docs/contact-center-http-connector](https://developer.webex.com/webex-contact-center/docs/contact-center-http-connector).

### The Webex Contact Center API Connector in Action

One practical application of the Webex Contact Center API Connector is enhancing customer service by leveraging the [Search API](https://developer.webex.com/webex-contact-center/docs/getting-started-with-search-api) to improve call routing. Imagine a scenario where a customer calls back the contact center and it's beneficial for them to speak with the last agent they interacted with. By utilizing the Search API within the Webex Contact Center Flow Designer, you can efficiently look up the last agent the caller spoke with and automatically add the caller to that agent's call queue. This not only personalizes the customer experience but also improves resolution times by allowing agents who are already familiar with the customer's history to assist them more effectively. The Webex Contact Center API Connector makes this task much simpler than it used to be.

#### Webex Contact Center API Connector Setup

Setting up the Webex Contact Center API Connector is straightforward. To get started, follow these high-level steps:

1. Login to [Webex Control Hub](https://admin.webex.com/) with an account that has one of the following privileges: 
    - Full Administrator
    - External Admin with Full Administrator Access
    - Contact Center Service Administrator
1. Create a Webex Contact Center API Connector:
    1. Navigate to **Contact Center** -> ***Integrations*** -> **Connectors** and select **Set Up** or **Add More** under the **Webex Contact Center Connector**:
        ![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt806817f8fa4b14da/wxcc-http-connector-blog-2.png)
    1. Give your connector a name that will be used in Flow Designer, choose the level of access (read or read/write), and authorize the connector:
        ![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt0e579ca71a8ad85c/wxcc-http-connector-blog-3.png)
    1. Your connector is ready, we will use the “WxCC Search Connector” shortly:
        ![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt1ca3b97177bc5939/wxcc-http-connector-blog-4.png)

<br/>

#### Flow Overview

This is the flow that will route a caller to their previous agent. It has a lot of steps, but we will break them down:

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt9f6b076a34f980dd/wxcc-http-connector-blog-5.png)

1. When a new call comes in, we are going to get and set a few variables:
    - `currentTime` is set to the current time of the call.
    - `goback_by_a_day` is set to the current time minus a day.
    - `ANITrim` is set to the caller's current number without the country code.
1. Use the Search API to find which agent this caller talked to recently.
1. Set the `Agent_ID` based on what was found via the Search API
1. Send to the agent's queue if found.
1. Send to main queue if the agent is not available.

<br/>

#### Calling the Search API with the New Connector

The magic comes in at step 2 where we are calling the Search API. In our **HTTPRequest** activity, we will be doing things a little differently with the WebexCC API Connector:

1. The general settings stay the same, label and description.
    ![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltfe694014a30d66c5/wxcc-http-connector-blog-6.png)
1. On the HTTP Request Settings, we are going to enable **Use Authenticated Endpoint**. Then, we will choose the **WxCC Search Connector** we just created.
    ![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt6dcb4954513d0a59/wxcc-http-connector-blog-7.png)
1. Add the path to the API endpoint in **Request Path**. Note that this is a **PATH** not a **URL**; the connector handles the main part of the URL for us. We are making a request to the Search API so we are using the `/search` path.
    ![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt8a145bc7766584b3/wxcc-http-connector-blog-8.png)
1. Finally, we store the results of the Search API in the **Agent_ID** flow variable.

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte8a6dc84355743e6/wxcc-http-connector-blog-9.png)

We can now use the **Agent_ID** variable to route to that agent if the information was found!

This was just a basic use case, but there are many different reasons for using our Webex Contact Center APIs within flows, and with the new Webex Contact Center API Connector, it is easier than ever!

### Best Practices for Using the Webex Contact Center API Connector

Keep in mind the following best practices when using the Webex Contact Center API Connector:

- **Access Rights**: Choose **Read-Only** access rights if you intend on making only `GET` API calls. **Read-Write** connectors should be reserved for flows in which you intend on making `UPDATE`/`POST`/`PUT` API calls.
- **Avoid Storing Sensitive Information**: Ensure no sensitive response data is stored in the flow logs.
- **Rate Limiting**: Be aware that API calls from the Flow Designer are rate limited. Handle potential 429 errors gracefully.
- **Error Handling**: Use a **Case** Activity to handle all error codes listed in the API definition. Optimize your flows by creating sub flows to manage error cases effectively. 

Learn more about [common API errors](https://developer.webex.com/webex-contact-center/docs/common-api-errors).

By following these guidelines and leveraging the Webex Contact Center API Connector, you can create robust, customized workflows that enhance your contact center's efficiency and effectiveness. Start exploring the possibilities today!

### Where to Go Next

For more detailed instructions and examples, visit the [Webex Contact Center for Developers Portal](https://developer.webex.com/webex-contact-center/docs).

### Need Some Help? We Got You Covered!

We are excited to provide you with support for these features. If you need help, the [Webex Developer Support Team](https://developer.webex.com/support) is standing by and happy to assist. You can also start or join a conversation on the [Webex for Developers Community Forum](https://cs.co/WebexDeveloperCommunity).
