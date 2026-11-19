---
type: Article
title: Enhancing Webex Contact Center Widgets with Dynamic $STORE Variables
canonical_url: https://developer.webex.com/blog/enhancing-webex-contact-center-widgets-with-dynamic-store-variables
content_type: blog
date: '2024-05-31'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/enhancing-webex-contact-center-widgets-with-dynamic-store-variables)

As Webex developers, creating a productive and collaborative workspace for Contact Center agents is paramount. One of the key features that can significantly bolster this effort is the use of dynamic `$STORE` variables. These variables allow for real-time customization of agent widgets based on contextual data provided by the Webex Contact Center platform.

Today, we're exploring the transformative potential of `$STORE` variables and how they can be integrated into agent widgets for a more connected and efficient workspace.

### Harnessing $STORE Variables for Tailored Agent Experiences

`$STORE` variables serve as conduits of context, carrying vital information that can be rendered in real-time within your customized widgets. They capture everything from user settings to customer data, equipping agents with a wealth of information at their fingertips.

Utilizing these dynamic variables within your widgets can create a responsive and engaging environment for agents, leading to improved customer interactions and streamlined workflows.

### Real-World Applications and Advantages

Incorporating `$STORE` variables into your widgets can take many forms. Here are some scenarios where they can make a real difference:

- **Adaptive Interface Elements**: Widgets that respond to the `$STORE.app.darkMode` variable can automatically adjust their theme to align with the agent’s display preferences, reducing visual fatigue and enhancing focus.
- **Contextual Agent Insights**: Variables like `$STORE.agent.agentName` can pull in agent names for a personalized touch that fosters connection and rapport from the moment the interaction begins.

The introduction of `$STORE` variables into widgets not only customizes the agent's environment but also paves the way for:

- **Optimized Agent Workflows**: With less time spent navigating for information, agents can focus more on the customer.
- **Targeted Customer Solutions**: Access to real-time data enables agents to provide more accurate and personalized service.
- **Elevated Productivity**: A workspace that adapts to both agent and customer needs leads to more efficient operations.

`$STORE` variables are updated in real-time so that your widgets are constantly up to date with the Webex Contact Center desktop. One thing to note, these `$STORE` variables are only available for Web Component widgets, not for iFrame widgets. For a walkthrough of building a Web Component widget, take a look at my previous blog: [Developing With Webex Contact Center Header Widgets: An RSS Feed Reader Example](https://developer.webex.com/blog/developing-with-webex-contact-center-header-widgets-an-rss-feed-reader-example).

### $STORE Variables: The Agents of Change

`$STORE` variables are the secret sauce that can transform an ordinary agent widget into a powerhouse of productivity and personalization. They provide a stream of real-time data that widgets can utilize to present information that is current and relevant to the task at hand.

Here's a rundown of the top-level `$STORE` variables and how they can be leveraged in agent widgets:

#### $STORE.agent

This namespace includes details about the agent such as their state (e.g., Available, Busy), skills, and queue membership. Widgets can use this data to show or hide features relevant to the agent's status or to provide alerts when their attention is needed elsewhere.

#### $STORE.agentContact

This variable holds information about the current customer interaction tasks. It contains details such as the list of tasks that are assigned to an agent at a given time. Widgets can use this information to prepare the agent with tools and information specific to the tasks they are assigned with.

#### $STORE.app

Application-level settings and preferences such as locale, theme, and layout configurations are housed here. A widget, for example, could adjust its language and theme to match the agent's settings, ensuring a consistent experience across the Contact Center platform.

#### $STORE.auth

Here we find authentication-related data like the agent's token. This data is crucial for widgets that need to access external systems or APIs securely on behalf of the agent, ensuring that sensitive information is handled properly.

#### $STORE.generalNotifications

General notifications encompassing system alerts and other important messages are available within this variable. Widgets designed to keep agents informed can tap into this stream of notifications, making sure that agents are aware of system-wide announcements or updates.

#### $STORE.dynamic

Determines whether the Desktop is loaded in the connector view (smaller viewing area) or desktop view (larger viewing area).

### Integrating $STORE Variables: An Overview

<br/>

#### Step 1: Grasp $STORE Variables

Begin by getting to grips with the available `$STORE` variables. Familiarize yourself with their functionality and potential applications by examining the Webex Developer [documentation](https://developer.webex.com/webex-contact-center/docs/desktop#get-started).

#### Step 2: Configure the layout file

Your widget's behavior is influenced by the `layout.json` file. This is where you define which `$STORE` variables to pass through. Here’s a sample `layout.json` Configuration:

```json
{
  "comp": "custom-widget",
  "script": "http://localhost:8000/custom-widget.js",
  "properties": {
    "theme": "$STORE.app.darkMode"
  },
  "attributes": {
    "agent": "$STORE.agent.agentName"
  }
}
```

Note that you can pass both attributes and properties to your Web Component. To read about the differences, [Open Web Components has a handy article](https://open-wc.org/guides/knowledge/attributes-and-properties). For variables that are in flux, like the agent status, I recommend utilizing properties as Web Components make it easier to adjust to property changes.

### Conclusion: An Invitation to Innovate with $STORE Variables

The opportunity to elevate your Contact Center widgets through `$STORE` variables is exciting and boundless. By tapping into these dynamic data points, you create an environment that's not just reactive but predictive, offering agents an unparalleled level of support.

While I’ve only highlighted some of the top-level `$STORE` variables, documentation for all of the variables can be found in the [developer guide](https://developer.webex.com/webex-contact-center/docs/desktop#get-started). For more information on custom widgets, see the [Desktop Layout](https://www.cisco.com/c/en/us/td/docs/voice_ip_comm/cust_contact/contact_center/webexcc/SetupandAdministrationGuide_2/b_mp-release-2/b_cc-release-2_chapter_011.html#topic_8230815F4023699032326F948C3F1495) section in the Provisioning chapter of the Cisco Webex Contact Center Setup and Administration Guide.

**Embark on your journey with `$STORE` variables and witness the transformation of your Contact Center widgets. We're eager to hear about your creations and the positive impact they have on agent and customer experiences alike. Let's shape the future of Webex Contact Center customization together!**
