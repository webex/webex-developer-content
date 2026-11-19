---
type: Article
title: Unlocking the Power of Custom Widgets in Webex Contact Center
canonical_url: https://developer.webex.com/blog/unlocking-the-power-of-custom-widgets-in-webex-contact-center
content_type: blog
date: '2023-11-14'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/unlocking-the-power-of-custom-widgets-in-webex-contact-center)

Welcome to the world of Webex Contact Center and the exciting realm of widget development. In today's digital age, customer service has evolved, and creating seamless, efficient, and customer-centric experiences is more important than ever. One powerful way to achieve this is by crafting custom widgets for your Webex Contact Center platform. These small yet mighty applications can transform how your agents interact with customers, improving productivity, and ultimately leading to more satisfied clients. In this blog, we'll delve into the art and science of widget development for Webex Contact Center, exploring the possibilities and best practices that can take your customer service to the next level.

In the coming weeks, we're thrilled to embark on an exciting journey through a comprehensive blog series dedicated to building widgets for Webex Contact Center. We recognize that developing these widgets involves various aspects of customization, and we're here to guide you through each one. By the end of this series, you'll have a deep understanding of how to leverage these widget types to optimize your Webex Contact Center and provide exceptional customer service. Let's dive into the exciting world of widget development!



> **Info**
>
> Dive even deeper with the technical documentation on [Webex Contact Center Widgets](https://www.cisco.com/c/en/us/td/docs/voice_ip_comm/cust_contact/contact_center/webexcc/SetupandAdministrationGuide_2/b_mp-release-2/b_cc-release-2_chapter_011.html#Cisco_Concept.dita_a9771889-dbb1-4760-823e-cbb2536a2bda).



### Areas of Customization

Throughout this series, we'll explore four key areas of customization: Header Widgets, which allow you to seamlessly integrate essential information at the top of your Contact Center interface; Custom Page Widgets, which give you the creative freedom to design tailored pages within the Contact Center; Persistent Widgets, for maintaining real-time information across the user's workflow; and Headless Widgets, providing the flexibility to build and control widgets externally.

#### Header Widgets

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt9f30de1fe640d1ed/introducing-wxcc-widgets-2.png)

Header Widgets within Webex Contact Center are a powerful tool for enhancing user experience. They allow developers to display inline information and create drop-down menus for quick access to crucial features. This prime space is perfect for adding custom items tailored to the needs of both agents and supervisors. Developers can even include informative tooltips that provide guidance when users interact with these widgets.

For a real-world example, check out the image above, showcasing a Header Widget labeled "Button T" in the Agent Desktop's horizontal header. In our upcoming blog series, we'll explore how to create and customize Header Widgets, enabling you to optimize this vital area, and making your agent and supervisor workflows more efficient and user-friendly. Stay tuned for practical insights and guidance!

#### Navigation (Custom Pages) Widgets

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt5145bf14b25ac1e9/introducing-wxcc-widgets-3.png)

Custom Pages are a fundamental aspect of the Webex Contact Center Desktop interface, residing within the workspace pane. These pages provide a structured canvas for arranging information and tools essential to agents and supervisors. To access Custom Pages, users can simply click on icons located on the navigation bar, offering a seamless and intuitive experience.

One of the key considerations when developing Custom Widgets for these pages is to enhance navigation. This involves adding items to the vertical navigation bar, which serve as signposts directing users between the home page and specific Custom Pages. This ensures a logical flow through the interface, optimizing productivity and usability. As shown in the image above, the highlighted vertical navigation bar plays a pivotal role in guiding users to the right Custom Pages, where they can interact with a range of custom widgets, streamlining their workflow and delivering a more efficient user experience. Stay with us in this blog series, as we explore the intricacies of creating and configuring these Custom Page Navigation Widgets, providing you with the knowledge to tailor your Contact Center to your specific requirements.

#### Persistent Widget

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt7a0186e4e429a8e5/introducing-wxcc-widgets-4.png)

Persistent Widgets are a vital component of Webex Contact Center, designed to provide users with continuous access to real-time information. These widgets remain visible throughout a user's workflow, ensuring that important data, notifications, or tools are always at their fingertips. Imagine having critical statistics, alerts, or even a live chat interface accessible without the need for constant navigation. 

One compelling use case for Persistent Widgets is within a contact center environment. Agents can benefit greatly from a persistent widget that displays real-time queue statistics, such as the number of customers waiting, average wait time, and current agent availability. This allows agents to monitor the situation and make informed decisions instantly. For instance, if the queue is getting congested, agents can proactively switch to a different communication channel or take other actions to improve customer service. Throughout this blog series, we'll explore how to create and customize Persistent Widgets, enabling you to harness the power of real-time data within your Contact Center interface. Stay tuned for insights and practical guidance!

#### Headless Widget

Headless Widgets in Webex Contact Center represent a unique approach to widget development. Unlike traditional widgets, they don't have a graphical interface within the agent or supervisor desktop. Instead, they serve as a powerful bridge to external applications and processes, enabling developers to customize and extend the functionality of the Contact Center interface more abstractly.

A compelling use case for Headless Widgets is their integration with CRM (Customer Relationship Management) systems. These widgets can seamlessly connect with external CRM platforms, allowing agents to access customer profiles, historical data, and relevant information directly from the Contact Center interface. This integration streamlines workflows, ensuring that agents have a 360-degree view of the customer during interactions, ultimately leading to more personalized and efficient customer service. In the upcoming segments of our blog series, we'll delve into the world of Headless Widgets, exploring how to build, integrate, and maximize their potential to create a tailored and dynamic Contact Center environment. Stay tuned for in-depth insights and practical guidance! If you're ready to go now, check out [this open-source sample headless widget](https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/widget-samples/headless-crm-widget-sample).

### Types of Widgets Development

Now that we've covered the essential widget customization areas within Webex Contact Center, let's turn our attention to two specific categories of widgets that developers can build: iFrame Widgets and Web Components.

#### iFrame Widgets

iFrame Widgets offer a gateway to incorporate external content and applications seamlessly into the Contact Center interface. Developers can embed web pages, applications, or content from external sources within an [iFrame](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/iframe). This capability opens the door to a wide range of integrations, allowing you to bring in third-party tools, custom dashboards, or virtually any web-based content. iFrame Widgets are a fantastic option when you need to enrich the Contact Center environment with information or functionality that resides outside of the core platform. [A sample iFrame Widget can be found on our GitHub](https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/widget-samples/iframe-widget-sample).

#### Custom (Web Component) Widget

[Web Components](https://developer.mozilla.org/en-US/docs/Web/API/Web_components), on the other hand, offer a more modular and reusable approach to widget development. They are custom-built, self-contained elements that encapsulate both the structure and behavior of a widget. These components can be easily shared and inserted into different parts of the Contact Center interface. Web Components provide a more structured and standardized way to create widgets, enhancing code maintainability and enabling efficient reuse of widgets across various pages and contexts.

In our upcoming blog posts, we'll explore how to create and customize both iFrame Widgets and Web Components, giving you the tools to enrich your Contact Center interface with tailored, external content and modular, efficient widgets. Whether you're looking to seamlessly integrate external resources or build a library of reusable elements, these widget types provide diverse options for enhancing your Contact Center's capabilities. Stay with us as we dive deeper into widget development in the following articles! 

### Configuring Custom Widgets with the Layout File

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt2793aa4e57370068/introducing-wxcc-widgets-5.png)

A fundamental aspect of building and configuring custom widgets in Webex Contact Center is the use of the `layout.json` file. This file acts as a central hub for defining the layout and arrangement of custom widgets within the Contact Center interface. It offers a structured and efficient way to tailor the user experience, ensuring that widgets are positioned precisely where they are needed.

The `layout.json `file allows developers to specify not only the placement of widgets but also their properties, such as size, visibility, and behavior. This level of control is invaluable when creating a highly customized Contact Center environment. Whether you're working with Header Widgets, Custom Page Navigation Widgets, Persistent Widgets, or Headless Widgets, the `layout.json` file serves as the blueprint for crafting a user-centric interface that meets your organization's specific needs. In our upcoming blog posts, we'll guide you through the process of configuring custom widgets using this versatile file, providing you with insights and practical tips to create a Contact Center environment that optimally supports your team's workflow and customer interactions. Get started with the [technical documentation](https://www.cisco.com/c/en/us/td/docs/voice_ip_comm/cust_contact/contact_center/webexcc/SetupandAdministrationGuide_2/b_mp-release-2/b_cc-release-2_chapter_011.html#topic_BF0EBDF65DCB0A552164D6306657C892) and stay tuned for detailed instructions and best practices!

### Empowering Widgets with Data

One of the key strengths of custom widgets in Webex Contact Center lies in their ability to access and interact with critical data, providing agents and supervisors with valuable insights and tools to enhance customer interactions. These widgets have the potential to tap into various sources of Contact Center data, delivering real-time information, historical context, and relevant details when and where they are needed.

Widgets can access Contact Center data through a well-structured and comprehensive API, along with the global JavaScript `STORE` for data. This `STORE` serves as a central repository for information, ensuring that data is easily accessible to widgets. Additionally, the Javascript SDK (Software Development Kit) provides developers with powerful tools and resources for integrating with the Contact Center's data sources, enabling widgets to pull in information about customer interactions, agent performance, queue statistics, and much more. This wealth of data empowers agents to provide more personalized and efficient customer service, making every interaction more informed and impactful.

Moreover, the ability to access Contact Center data within widgets opens the potential for automation and intelligent decision-making. Widgets can analyze incoming data and trigger specific actions or alerts, such as routing a call to a specialized agent based on customer history or escalating a support ticket when certain conditions are met. In our upcoming posts, we'll delve into the intricacies of data access for widgets, exploring how to harness these features, including the global JavaScript "store" and the JS SDK, to create a more data-driven and efficient Contact Center environment. Stay tuned for valuable insights and practical guidance on making the most of Contact Center data within your custom widgets!

### Wrapping Up

As we wrap up this blog, we've ventured into the world of Webex Contact Center widget development, exploring the versatility and potential of various widget types. From Header Widgets to Headless Widgets, we've uncovered ways to enhance user experiences, streamline workflows, and access critical data. 

Before you embark on your widget development journey, we'd like to note that getting started is easy. To experiment, test, and refine your custom widgets, it may be a good idea to request a [developer sandbox](https://developer.webex.com/webex-contact-center/docs/sandbox_cc) from the [Webex Contact Center Developer Portal](https://developer.webex.com/webex-contact-center/docs). This is the perfect environment to kickstart your development process. There is also a fantastic [Desktop Developer Guide](https://developer.webex.com/webex-contact-center/docs/desktop) on the portal for you to follow. There are also tons of [sample widgets in our WebexSamples GitHub organization](https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/widget-samples).

Custom widgets offer a pathway to creating a Contact Center environment tailored to your unique requirements, and we're excited to see the innovations you'll bring to the table. Stay tuned for more in-depth discussions and practical advice in our upcoming posts and thank you for joining us on this exploration of widget development!

### Need Some Help? We Got You Covered!

We are excited to provide you with support for these features. If you need help, the [Webex Developer Support Team]("/support) is standing by and happy to assist. You can also start or join a conversation on the [Webex for Developers Community Forum](https://cs.co/WebexDeveloperCommunity).
