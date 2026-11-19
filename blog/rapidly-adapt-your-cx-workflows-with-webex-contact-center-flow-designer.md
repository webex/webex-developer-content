---
type: Article
title: Rapidly Adapt Your CX Workflows With Webex Contact Center Flow Designer
canonical_url: https://developer.webex.com/blog/rapidly-adapt-your-cx-workflows-with-webex-contact-center-flow-designer
content_type: blog
date: '2024-08-07'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/rapidly-adapt-your-cx-workflows-with-webex-contact-center-flow-designer)

> **Info**
>
> This blog was co-authored by Naveen Kumar H N



In today’s fast-paced technology landscape, customer experience (CX) is a key differentiator for enterprises. The ability to adapt and evolve CX workflows rapidly and seamlessly, introducing the most effective capabilities for customers, can make the difference between leading the market and lagging. Enterprises are eager to learn how to implement these changes to production workloads safely and effectively while adhering to controlled enterprise change management processes. Flows are like any software artifacts that need to go through a well-defined pipeline process involving planning, building, and testing.

Over the last several quarters, the Webex Contact Center Flow Designer platform has introduced several features: Flow Versioning, Percentage Allocation of Flow Traffic, Subflows and Dynamic Variable Support - which empower developers and administrators to implement change management processes effortlessly. This blog explores the context of these capabilities, discusses use cases, and illustrates their impact on evolving your CX journey; Take advantage of the latest capabilities that Webex Contact Center has to offer.

### Evolution of Change Management

Historically, change management in CX workflows (previously known as contact center scripts) has been a delicate balancing act. The need to introduce new features and improvements had to be weighed against the risk of disrupting existing production workloads. Techniques like Blue-Green deployments and A/B testing revolutionized this process in broader disciplines like software development:

- “Blue-Green deployments” involve maintaining two environments (Blue and Green) to allow seamless transitions between versions.
- “A/B testing” enables comparison between different versions to determine the most effective approach.

CX workflows should be no different. Webex Contact Center Flow Designer has integrated these methodologies into the platform, providing developers with the tools needed to manage changes with precision and confidence. These methods ensure that updates in your workflows can be rolled out gradually, maximizing value while minimizing risk and optimizing performance.

Flow Versioning enables developers to confidently perform Blue/Green deployments using "Dev," "Test," or "Live" versions, ensuring seamless transitions and rollback to previous versions without downtime. Flow Percentage Allocations allows you to A/B test different experiences, feature sets, or a combination of the two. Combining these with subflows and dynamic variable support for activities, you can build a robust pipeline setup for your teams, to test multiple flavors of the flow without duplicating the overall experience.&#xa0;&#xa0; We will look at these features in detail.

### Flow Versioning – Streamlining Development and Deployment

Flow Versioning introduces the ability to apply version labels to a flow, offering unprecedented flexibility in developing, testing, and deploying new enhancements to your CX. This feature enables the creation of a formally defined, pipeline driven promotion process from development to production, facilitating Blue-Green deployments for CX flows.

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt1ff8754b3268fc45/flowdesigner_evolvecx-2.png)

Flow Versioning allows switching environments on the Entry Point level

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt2bc6ce268be9eea5/flowdesigner_evolvecx-3.gif)

*Applying a Version Label to a Flow*

#### Using Flow Versioning

<br/>

1. **“Dev” (Development)**: Begin by creating and testing new flow enhancements by assigning the “Dev” Version Label to your flows. Attach the 'Dev' version label of the Flow to a test Entry Point to ensure it does not impact production calls.
1. **“Test” (Staging)**: Once the flow is thoroughly tested, promote it to the “Test” environment by applying the “Test” version label while publishing the flow. This creates an additional copy of the flow for staging that allows for further validation without affecting live customer interactions.
1. **“Live” (Production Deployment)**: After successful testing, the flow can be promoted to the production environment by assigning the 'Live' version label. This controlled rollout minimizes risks and ensures a seamless transition.

The above versions can be assigned from the Entry Point for all contacts, to the Flow version label that is being used – allowing for maximum flexibility. Suppose you want to introduce an update to the Flow - change the flow and publish it again with the Dev tag, preventing any impacts to Live traffic. Go through the promotional process outlined above.

Flow Versioning not only supports Blue-Green deployments but also creates a structured pipeline for continuous integration and continuous deployment (CI/CD), ensuring that new enhancements are delivered efficiently and reliably.

For more information on Flow Versioning, see: [Flow Versioning for Flow Designer](https://help.webex.com/en-us/article/n5595zd/Webex-Contact-Center-Setup-and-Administration-Guide#flow-versioning)

### Percentage Allocation – Mastering Traffic Distribution &amp; A/B Testing

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blta744fc8f5358f2fd/flowdesigner_evolvecx-4.png)

*Percentage Allocation of traffic follows a Weighted Round Robin distribution*

The Percentage Allocation feature empowers developers to distribute call traffic across different branches within a flow. This capability is instrumental in implementing A/B testing methodologies, enabling a weighted allocation of traffic to various experiences – while providing valuable data for reporting and feedback loops.

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt10352c956fdcf61e/flowdesigner_evolvecx-5.png)

*40-30-30% Traffic Split between DTMF, TTS and Bots (Virtual Agents)*

Developers can now allocate specific percentages of calls to different queues, or experiment between traditional IVR, Next-Generation Text-to-speech (TTS) or conversational virtual agents in the contact paths. This capability also allows trying out different post-call surveys, or Agent Screen pop applications to see what impact it has on Experience metrics for both callers and agents. Using this activity effectively allows for granular control and optimization of CX workflows over time, using feedback loops via reporting.

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt2e13108af0462d91/flowdesigner_evolvecx-6.png)

*70-30% traffic split for Agent Screenpops (Old vs New Application experiences for agents)*

#### Using Percentage Allocation

In the example below, we are A/B testing two contact paths between a traditional menu and the all-new Cisco Virtual Agents available on Flow Designer.

Global Variables assigned to the output of the nodes enables us to report directly on the contacts that traversed specific paths, helping us compare the business outcomes achieved, for example, the self-service duration, CSAT or NPS with the caller between the two or more experiences.

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt11f1ad5e60b1cae5/flowdesigner_evolvecx-7.png)

*Capturing custom data on chosen paths for reporting*

**Recommendations**

1. **Define Allocation Percentages**: Within the Flow Designer, specify the percentage of call traffic to be directed to each branch. For instance, allocate 50% to the existing flow and 50% to a new experimental flow.
1. **Monitor and Analyze**: Continuously monitor the performance of each branch to gather insights and compare results using Global Variables and an Analyzer Report to calculate the business impact. This data-driven approach facilitates informed decision-making.
    For more information on creating Analyzer Reports, see: [Create a Custom Visualization on Analyzer](https://help.webex.com/en-us/article/tajemk/Cisco-Webex-Contact-Center-Analyzer-User-Guide).
1. **Adjust Allocations**: Based on the analysis, adjust the percentage allocations dynamically. For instance, increase the traffic to the better-performing branch and decrease or deactivate the other.

Percentage Allocation allows for precise control over CX workflows, enabling enterprises to test new features and improvements on a small scale before a full rollout, thereby reducing risk and enhancing overall performance.

For more information on Percentage Allocation see: [Percentage Allocation for Flow Designer](https://help.webex.com/en-us/article/n5595zd/Webex-Contact-Center-Setup-and-Administration-Guide#task-template_2da0579d-5c10-4021-8b5d-61e8220bf5da).

### Subflows – Enhancing Modularity and Reuse

Subflows introduce a modular approach to building and managing complex CX workflows – especially when packaging a new capability and wanting to reuse it across your flows.

Developers can create independent logical functionalities as Subflows and reuse them across multiple main flows. This modularity simplifies the development process, enhances collaboration among teams, and ensures consistency across the organization.

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt05fbbd0a2a5b1431/flowdesigner_evolvecx-8.gif)

*Subflows are activities on the Flow Canvas*

A good example of this is a new Subflow pointing to a new HTTP(S) endpoint, or a subflow using the new Virtual Agent activity – allowing to test new >API services or new AI agents in the contact path, respectively.

#### Best Practices for Subflows

<br/>

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt11dea84ff6870133/flowdesigner_evolvecx-9.png)

*Common Subflows in use – BusinessHours, QueueTreatment, CollectCallerInfo, etc.*

1. **Create Independent Functionalities**: Develop subflows for specific tasks or functionalities that can operate independently within the main CX flow. Some examples include: Business Hour checks, Common Queue treatments and common API calls (HTTPS) to external services.
1. **Reuse Across Main Flows**: Integrate these subflows as new activities into various main flows as needed, ensuring that common functionalities are consistent and easily manageable.
1. **Collaborate Effectively**: Different teams can work on various subflows simultaneously, streamlining the development process and fostering collaboration. Develop them independently in parallel – integrate them in one main flow.

Subflows allow developers to break down complex flows into manageable parts, promoting modularity and reusability – and most importantly saves time through increased efficiencies.

The setting “Propagate changes to all flows” allows for easy cascading of changes to all parent flows. Disabling this setting when making a subflow change ensures that a change in one subflow does not disrupt all the flows consuming it.

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blta3432e98fc280768/flowdesigner_evolvecx-10.png)

*Choosing to pull the latest updates from Subflows as a Setting.*

For more information on Subflows see: [Subflows for Webex Contact Center Flow Designer](https://help.webex.com/en-us/article/n5595zd/Webex-Contact-Center-Setup-and-Administration-Guide#concept-template_2812e465-bde2-4bf8-b133-b64bbddff95b).

### Dynamic Variable Support – Enabling Adaptive Flows

Dynamic Variable support allows developers to specify the behavior of activities within a flow through variables. This enhancement enables the creation of highly adaptable and reusable flows. By defining activities via dynamic variables, developers can tailor flows to different business verticals, and change their behavior dynamically for different environments (Dev, Test, Live), altering their functionality based on data injected into the flow at runtime.

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt9fb3ed33bdac7762/flowdesigner_evolvecx-11.gif)

*Using Dynamic Variables in activities such as Business Hours, GoTo Flows, GoTo Entry Points*

#### Implementing Dynamic Variables

<br/>

1. **Define Variables**: Create dynamic variables to control various aspects of the flow’s behavior.
1. **Apply Variables in Activities**: Use these variables within activities to modify their functionality based on the current environment or real-time data.
1. **Adapt Flows Dynamically**: Adjust the values of these variables as needed to adapt the flow to different conditions or requirements.

Dynamic Variable support enhances the flexibility and adaptability of CX workflows, allowing developers to create flows that can evolve and respond to changing circumstances without the need for extensive rewrites. It also minimizes the overall number of flows or subflows created, significantly easing the manageability of flows.

For more information on using Dynamic variables in Flow activities, see: [Dynamic Variable support in Flow Designer Activities](https://help.webex.com/en-us/article/n5595zd/Webex-Contact-Center-Setup-and-Administration-Guide#Cisco_Concept.dita_5ba6029e-c256-4c16-8fbf-40f8370bd968).

### Comprehensive Use Case: Implementing New AI-powered Virtual Agents

Let us consider a comprehensive use case where an enterprise implements a new AI-powered Cisco virtual agent to improve its customer support experience.

#### Step 1: Developing the Virtual Agent

Using Flow Versioning, the development team creates a new flow for the virtual agent in the “Dev” environment. They label this version as “Dev” and conduct extensive testing to ensure that the virtual agent can handle various customer queries effectively.

#### Step 2: Testing in a Controlled Environment

Once the virtual agent flow is stable, it is promoted to the Test environment and labeled 'Test.' Here, a subset of real customer interactions is routed to the virtual agent using the Percentage Allocation feature. By allocating a small percentage of calls to this flow, the team can gather valuable performance data and customer feedback without impacting live interactions.

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte9ff554e9fe45f40/flowdesigner_evolvecx-12.png)

*Sending 40% of the traffic to a new AI bot (Virtual Agent) and 60% to traditional IVR.*

#### Step 3: Analyzing Results and Adjusting

The team monitors the virtual agent’s performance in the Test environment, using data to refine and improve the flow. Adjustments are made dynamically using the Dynamic Variable support, allowing for real-time tweaks based on customer interactions and feedback. The output variables in the activity allow for reporting on these values in Global Variables. Global Variables are reportable on Analyzer as a part of all historical and real-time reports (these custom fields are automatically available as a part of the Contact Session records captured by the Webex Contact Center data platform).

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blta34ed939e49fdff9/flowdesigner_evolvecx-13.png)

*Activity Output variables allow reporting on the percentage and description per call.*

#### Step 4: Rolling Out to Production

Satisfied with the virtual agent’s performance, the team promotes the flow to the Live environment and labels it 'Live.' The Percentage Allocation feature is then used to gradually increase the traffic directed to the virtual agent, starting with a small percentage, and scaling up as confidence in the flow’s performance grows.

#### Step 5: Continuous Improvement

With the virtual agent now live, the team continues to monitor its performance and gather feedback. Subflows are used to modularize specific functionalities, making it easy to update and improve individual components of the virtual agent without disrupting the entire workflow.

### Advantage: Adapt and Futureproof

By leveraging Flow Versioning, Percentage Allocation, Subflows, and Dynamic Variable support, enterprises can achieve true enterprise-grade change management for their CX workflows while remaining future proof, continuously adapting their CX to the needs of the hour. These features enable:

1. **Controlled Rollouts**: Minimize risks by testing changes in smaller batches before full-scale deployment.
1. **Continuous Adaptation**: Continuously evolve CX workflows with data-driven insights from A/B testing.
1. **Enhanced Collaboration**: Improve collaboration among teams through modular subflows.
1. **Future-Proofing**: Introduce AI capabilities and other innovations in a controlled manner, ensuring readiness for future advancements.

<br/>

### Conclusion

Webex Contact Center Flow Designer’s new features—Flow Versioning, Percentage Allocation, Subflows, and Dynamic Variable support—represent a significant leap forward in CX change management. By adopting these capabilities, developers can implement changes with confidence, ensuring a seamless and optimized customer experience. These features provide the flexibility to test and refine new enhancements, control rollouts through precise traffic distribution, and build modular, adaptable workflows that can evolve with changing business needs.

With Flow Designer, enterprises can continuously adapt their CX workflows, integrate cutting-edge AI capabilities, and future-proof their customer interactions. Embrace these features today to transform your CX strategy, stay ahead of the competition, and deliver exceptional experiences that meet the ever-evolving expectations of your customers. Your journey towards a more agile, responsive, and customer-centric future begins here with Webex Contact Center Flow Designer.

### Need Some Help? We’ve Got You Covered!

We are excited to provide you with support for these features. If you need help, the [Webex Developer Support Team](https://developer.webex.com/support) is standing by and happy to assist. You can also start or join a conversation on the [Webex for Developers Community Forum](https://cs.co/WebexDeveloperCommunity).
