---
type: Article
title: 'Leveraging Service Apps for Secure and Scalable API Calls: A Guide for Admins and Developers'
canonical_url: https://developer.webex.com/blog/leveraging-service-apps-for-secure-and-scalable-api-calls-a-guide-for-admins-and-developers
content_type: blog
date: '2023-12-21'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/leveraging-service-apps-for-secure-and-scalable-api-calls-a-guide-for-admins-and-developers)

Today, we are going to explore [Webex Service Apps](https://developer.webex.com/docs/service-apps), particularly how they simplify authorizing org-level integrations for admins while making token consumption for making API calls secure and scalable for developers. 

For example, if you're an admin and you have an automated process internally, or if you're allowing a 3rd party developer to write an app that performs admin tasks for your organization, service apps can be incredibly useful by turning an admin-authorized integration into a virtual admin, limited by scopes selected in the developer registration process, to do tasks like automate provisioning, generate reports, and create meetings for an entire org. Furthermore, if an authorizing user leaves the company or changes their passwords, the Service App will continue to function, ensuring a smoother workflow. Any full admin can go into the control hub and disable or enable an available service app. 

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltc32bface822b007e/service-apps-blog--2.png)

Developers get most of the same tools that a Webex integration would provide when registered to start building out the OAuth 2.0 flow. The part that makes Service Apps beneficial for developers is that they can request admin authorization in the developer portal. This request makes the app available to admins in the Control Hub. Once the admin authorizes the application, the developer gains quick access to an access token and a refresh token without having to redirect users from their integration to the Webex ID broker, simplifying the authorization process. All the developer needs to do is use the [refresh token according to the integration documentation](https://developer.webex.com/docs/integrations#using-the-refresh-token) to maintain a valid set of access and refresh tokens. Please see [this sample code](https://github.com/WebexSamples/simple_service_app) for implementation. 

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltfcceb484eba7a473/service-apps-blog--3.png)


### Need Some Help? We Got You Covered!

We are excited to provide you with support for these features. If you need help, the [Webex Developer Support Team](https://developer.webex.com/support) is standing by and happy to assist. You can also start or join a conversation on the [Webex for Developers Community Forum](https://cs.co/WebexDeveloperCommunity).
