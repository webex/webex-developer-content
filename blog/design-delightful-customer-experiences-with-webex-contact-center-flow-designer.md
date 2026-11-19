---
type: Article
title: Design Delightful Customer Experiences with Webex Contact Center Flow Designer
canonical_url: https://developer.webex.com/blog/design-delightful-customer-experiences-with-webex-contact-center-flow-designer
content_type: blog
date: '2024-04-23'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/design-delightful-customer-experiences-with-webex-contact-center-flow-designer)

Today's customers expect a certain standard when interacting with a Contact Center. They expect a personalized experience that acknowledges their preferences, an understanding of their issue, and a swift, efficient resolution without repetitive information or unnecessary checks and processes. Furthermore, they prefer not to be shuffled between different teams due to a lack of available information, often leading to speaking with multiple agents to resolve their issues.

By leveraging deep integrations with existing enterprise data, developers can differentiate customer experiences for Contact Centers by tying together disparate enterprise systems with the help of a single orchestration platform, leading to exceptional customer satisfaction.

Webex Contact Center is powered by the Flow Designer platform for orchestration and automation, enabling developers to design robust, data-driven integrations effortlessly through a no-code low-code interface.

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt5e4e39bc8d6490a2/flow-designer-data-for-devs-blog-2.png)

With its intuitive, visual canvas, Flow Designer simplifies the development process, encouraging collaboration between developers and business stakeholders, enabling the creation of applications that provide superior customer experiences.

This article details the specific interfaces offered by Flow Designer for integrations, and demonstrates how to incorporate personalization at every step, harnessing the platform's full capabilities.

### Integrating Data Intelligence into Flow Designer

To provide a seamless customer experience for Contact Center callers, various stages in a contact flow can leverage deep integrations for personalization:

- **Caller Identification:** Quickly identify who the caller is and the reason for their call with the least amount of caller input, re-prompting, or tiring menus.
- **Customer Authentication:** Workflows to ensure the customer’s authenticity is verified with the business, to complete the transaction.
- **Problem Identification:** Efficiently pinpoint their issue without subjecting them to lengthy self-service navigation or extended hold times.
- **Data Retrieval Specific to the Problem:** Gather all the relevant data needed automatically to resolve their issue.
- **Intelligent Routing Using Insights from Data:** Direct the caller to the appropriate expert swiftly, ensuring that all pertinent information is readily available, before, during, and after the interaction with the bot or the agent.
- **Post-Contact Actions and Intelligence:** Validate the caller's intent and how the service could have been improved. Automate actions within backend systems after concluding a call.

The Flow Designer platform features a data-driven orchestration layer at its core, enhancing the Contact Center experience by making it more conversational and personalized. This involves selecting the optimal agent pools or queues and providing agents with key information, coupled with the capability to orchestrate post-call actions for callers.

At a high level, Flow Designer can transform standard contact flows into highly personalized interactions for each caller. It achieves this by utilizing deep integrations with existing enterprise applications and tailoring experiences to individual caller profiles. The platform leverages intelligent data about the caller for custom orchestration, can exchange this data with virtual agents (bots), can employ intelligent routing through data-driven agent selection, equipping agents with the necessary context, and orchestrating post-contact actions with event flows that leverage connected data payloads.

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt717d2731fa076e72/flow-designer-data-for-devs-blog-3.png)

Let us understand the interfaces that serve as points of integration when designing flows.

### Interfaces for Designing Intelligent Contact Flows

The Flow Designer canvas provides a range of activities (nodes) that can be connected to craft-specific experiences. Each activity includes an input and one or more outputs, depending on its functionality, and generates output variables that other activities can reference. Specific activities feature explicit interfaces for connecting to external systems and utilizing their data within the platform. These activities are seamlessly integrated to facilitate ongoing interactions with external applications throughout the contact lifecycle. A deep understanding of these interfaces unlocks use cases through integrations with external systems.

#### HTTP Activity

The HTTP Activity serves as the crucial point for interfacing with external systems. It provides the ability to target an external system and configure common “Custom Connectors” centrally on Control Hub, which can then be invoked across flows. Data can be retrieved from external systems using HTTP (GET) and shared with them using other supported verbs (PUT/POST/DELETE). Effective use of the HTTP activity can determine the success of the orchestration.

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt44b46c3c54aaab74/flow-designer-data-for-devs-blog-4.png)

For more information, see [Setting up Integration Connectors for Webex Contact Center Flow Designer](https://help.webex.com/en-us/article/7fuy63/Set-up-integration-connectors-for-Webex-Contact-Center).

#### Virtual Agent

The Virtual Agent (VA) activity enables the transfer of custom data from Flow to a virtual agent when initiating a bot within the orchestration. It allows passing custom data to the VA, connecting with 3rd party systems from within the VA, and finally retrieving data from the VA, along with the transcript of the bot interaction. Customizing bot interactions for each customer starts with the use of "Event State” and “Event Data" within the Virtual Agent activity. This allows developers to send custom data payloads to Virtual Agents, which can then personalize messages and carry out backend "fulfillment" actions using this data by integrating with external systems. When the call is escalated from the VA, control is passed back into Flow along with the data that was used within the VA. This is critical for a connected experience.

For more information, see [Configuring Virtual Agents on Webex Contact Center Flow Designer](https://help.webex.com/en-us/article/n6gaghu/Configure-Virtual-Agent-Voice-in-Webex-Contact-Center).

#### Dynamic Speech Activities

The Flow Designer's media activities, such as "Play Message," "Collect Digits," "Menu," etc., support dynamic text-to-speech (TTS), which enables the embedding of custom data within utterances for personalized interactions with callers. Using expressions to inject custom data effectively, along with Speech Synthesis Markup Language (SSML) to modify speech intonations, ensures personalization at the self-service stage of the call.

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blta1a79bfd265663be/flow-designer-data-for-devs-blog-5.png)

#### Queue Activities

The Queue activity enables the definition of Skills-Based Routing Queues, specifically in the configuration that uses "TEXT"-based skills. These can be used to route callers by leveraging custom data to identify suitable agents from the pool. Additionally, the “Queue To Agent” Activity can target the call to a specified agent using their ID or email, if data intelligence systems are leveraged to target a specific agent for the contact.

#### Screen Pop

The Screen Pop activity allows the embedding of custom data into the chosen webpage via query parameters, which accept custom variables defined in Flow. Customizing Screen Pops per agent, team, queue, and customer is possible by using conditional or case statements before a Screen Pop activity.

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt9a99cf6205719d48/flow-designer-data-for-devs-blog-6.png)

#### Subflows

The new Subflow activity enables developers to package reusable functionality for use in any number of flows by providing an easy method to include this functionality, pass inputs into the subflow, and return outputs to the main flow. This allows developers to build modular, reusable structures in the form of subflows, dynamically passing data to change the subflow's behavior. It also increases the efficiency of building flows while providing the same interfaces (HTTP, Collect Digits, Screen Pop) as connections to external systems within the subflow.

### Data Definitions for Effective Flow Design

Understanding the types of data accessible within Flow is essential for personalization. Flow provides an extensive list of variable types and data definitions, across various data types. Each of the variables are tailored to personalization and customization:

#### Local Variables

The cornerstone of personalization is defining custom variables to store business-specific and caller-specific information. Within Flow, local variables can be passed to other flows through the GoTo activity or the Subflow activity. They can also be displayed on the Agent Desktop, with customization options available in Flow Designer.

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltc9774fbf5db81d0b/flow-designer-data-for-devs-blog-7.png)

#### Global Variables

These special variables are defined at the organization level and used across multiple flows, particularly for reporting purposes. When set within a flow, global variables can be reported in Analyzer. Local variables can be collected by global variables for use in reporting.

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt28c35ad1b0fa40f4/flow-designer-data-for-devs-blog-8.png)

#### Caller Associated Data (CAD) Variables

Both local and global variables can be marked as Agent Viewable or Agent Editable, controlling their visibility and editability on the Agent Desktop. Agent viewable variables appear on the Desktop, whereas agent editable variables can be modified on the Desktop. Post-call event flows will then reflect the updated variable values for Flow Designer to use.

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltf2114c9b93bdd473/flow-designer-data-for-devs-blog-9.png)

#### Activity Output Variables

These variables are generated when a specific activity in Flow executes. They can be used alongside the user-defined local or global variables mentioned above.

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt8be8e49a19b33540/flow-designer-data-for-devs-blog-10.png)

#### Event Output Variables

The Flow Designer supports "Event Flows" that include a wide range of event activities triggered by various scenarios, such as when the flow selects an agent, an agent connects, or a call ends. These activities facilitate the orchestration of post-call actions. The event activities provide various output variables that can be utilized to personalize the experiences of both agents and callers.

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltd7c81da24e07a15f/flow-designer-data-for-devs-blog-11.png)

### Bringing it All Together: Add Intelligence to an Existing Flow

Assuming you have built your initial flow with simple messages, menus, and call queuing for the agent, let us enhance this design across each stage of the contact flow. Here is how we would incorporate personalization at every step, transforming the customer experience into a differentiated orchestration that is data-driven:

1. **Define a List of Custom Variables in Flow:** Use Flow Designer to construct a data structure comprising customer data, agent data, and other relevant contact center information. Create flow variables to identify the customer, understand their issue, and determine the appropriate agent for queuing – and leverage Global variables for reporting on flow-related events and actions.
1. **Leverage External Data Integrations Using the HTTP Activity:** Utilize the caller’s identification (ANI) or prompt the caller to input digits (e.g., an Account ID) to interface with an external API (Application Programming Interface) or CRM (Customer Relationship Management) system. Update external systems with call information throughout the contact's lifecycle to record the progress.
1. **Personalize Self-Service with Enhanced TTS (Text-To-Speech)** Leverage the power of data by building expressions into every speech activity with the help of `{{expressions}}` and SSML into text-to-speech messaging, personalizing prompts for customers for a more conversational experience.
1. **Provide the Right Information to the Agent:** Use Caller Associated Data (CAD) variables within Flow Designer and make them viewable and editable for the agent on the canvas. Reorder the Agent visible information and order of the variables on the Interaction pane settings.
1. **Surface the Right Applications to the Agent:** Employ the Screen Pop activity within the Event Flows to transmit the correct data into third-party applications, aiding in customer identification. Use the query parameters and expressions to “`{{inject}}`” custom data within the screen pop URLs.
1. **Leverage Widgets in the Desktop That Use These Variables:** Widgets on the desktop can access and manipulate variables passed from Flow Designer through the Desktop Layout and Desktop JS SDK. This integration means that the pertinent data from Flow Designer can be utilized by third-party widgets on the desktop, thus enhancing the data connectivity for agents.
1. **Utilize Event Flows for Post-Agent Actions:** Employ Event Flows and Event Output Variables after calls to orchestrate custom post-contact actions by coupling these with conditions, and case statements to tailor it per agent, per queue, or even per caller. By leveraging the Feedback activity in tandem with the HTTP activity, one can integrate with external applications that utilize post-contact data for insights and analytics following the interaction.

<br/>

### Conclusion

The Webex Contact Center Flow Designer provides a powerful platform for orchestrating and automating personalized customer interactions through deep data integrations and intelligent workflow automation. The use of HTTP activities, Virtual Agents, and Screen pops, along with Text-to-speech enabled activities enables developers to craft differentiated solutions that address specific customer needs while maintaining flexibility and scalability. By effectively leveraging these in different stages of the contact such as Customer Identification, Authentication, Payments, Problem Identification, Intelligent Routing, Desktop Integrations, and more, businesses can ensure a seamless and efficient customer experience that minimizes friction and enhances satisfaction. 

Looking ahead, Businesses should focus on enhancing data integration strategies, expanding the use of analytics for real-time decision-making within flows, and further customizing user experiences based on emerging customer trends. By doing so, companies can differentiate their CX and exceed customer expectations in an increasingly competitive landscape.

#### Ready to take your integrations to the next level?

Spin up a Webex Contact Center sandbox at [https://developer.webex.com/webex-contact-center/docs/sandbox_cc](https://developer.webex.com/webex-contact-center/docs/sandbox_cc) with live numbers and out-of-box flows today and experience the future of integration development with Webex Contact Center Flow Designer!

For more information on Flow Designer, register for our Webinar: Flow Designer for Developers at [https://developer.webex.com/webinars](https://developer.webex.com/webinars).
