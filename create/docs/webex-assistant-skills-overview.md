---
type: Guide
title: Webex Assistant Skills Overview
display_title: Overview
canonical_url: https://developer.webex.com/docs/webex-assistant-skills-overview
content_type: documentation
product_group:
- webex-suite
categories:
- create
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/webex-assistant-skills-overview)

Webex Assistant skills are applications that integrate and complement the Webex Assistant for Devices.

---



> **Warning**
>
> No new features are being added to Webex Assistant Skills and only skills added through May 2025 are directly supported by Cisco.



## Overview

Webex Assistant skills are applications that integrate and complement the Webex Assistant for Devices. Skills can be created by any user with a Webex account (get a free account at https://www.webex.com/team-collaboration.html). Skills are private to the organization associated with the user who created it. 

## What is the Difference Between the Webex Assistant and a Skill?

The Webex Assistant for Devices comes out-of-the-box with a wide array of voice-enabled functionality such as joining a meeting, orchestrating a call, and controlling settings on the device. A skill is a custom voice enabled functionality that may be enabled by the administrator for that organization's devices.

Additionally, whereas all native Assistant functionality is invoked with the standard `Ok Webex, <command>`, all skills have a name and matching invocation pattern that indicates the user's intent to engage with them specifically. The skill invocation pattern follows the structure: `Ok Webex, tell <Skill Name> <command>`, or `Ok Webex, ask <Skill Name> to <command>`.

## What Can You Build?

Developers can create unique, voice-driven applications that relay audio and web content back to Webex Board, Desk, Room, and Room Kit series devices. Assistant skills can also be used to give a voice to your existing business applications.

Here are some examples:

- [**Jarvis Room Controls Skill**](https://skills-developer.intelligence.webex.com/content/Jarvis-Skill.mp4): This example video showcases a home automation skill that controls various, real-life IoT connected device.
- [**Google Assistant Skill**](https://skills-developer.intelligence.webex.com/content/Google-Assistant-Skill.mp4): This example video shows a Webex Assistant skill powered by Google Assistant. Using the Skills API, Google Assistant can be enabled on Webex endpoints.
- [**Hermes Personal Assistant Skill**](https://skills-developer.intelligence.webex.com/content/Hermes-Skill.mp4): This example video showcases the Hermes skill. The skill extends the functionality of Webex Assistant and adds personal messaging and reminders.
- [**2048 Game Skill**](https://skills-developer.intelligence.webex.com/content/2048-Skill.mp4): This example video shows a Webex Assistant skill that brings the popular 2048 puzzle game to Webex Devices.


## How Should a Skill Behave?

Please refer to the [User Experience Design Guide for Webex Assistant Skill Developers](https://skills-developer.intelligence.webex.com/content/UX-Guide-for-skills.pdf) for a comprehensive guide for designing a voice enabled skill user experience.

## Skills Architecture Overview

We'll begin with a high-level overview of how the Webex Assistant skills platform works within the **Webex Assistant** architecture. The following image is an overview of the architecture:

![Webex Assistant Skills architecture](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltbdf7f475647eb961/618bf0affd0d2917d8cfbaf6/skills_architecture-1.png)

We'll start defining the different pieces of the system:

- **Actor**: A user invoking a Skill using the **Webex Assistant**. 
- **Webex Client**: A supported client that can run the **Webex Assistant**. In this case, it is a Webex Device.
- **Assistant Dialogue**: This is what gets the request and decides how to handle it.
- **Assistant NLP**: This is the part of the system that performs machine learning (ML) to analyze the **Actor's** query. Note that this is not used for skills. 
- **Assistant Skills**: This is a cloud service that manages skills created by third party developers like yourself.
- **Third-Party Skill**: This is a cloud service developed by a third-party. It's a service of its own, but it's registered with the **Assistant skills** service in order to be used by the **Webex Assistant**.

The flow works as follows:

1. The **Actor** wakes up Webex Assistant and requests the use of a skill. For example, the **Actor** can say: **OK Webex, tell Echo hello**.
2. The **Webex Client** then forwards that request to the **Assistant Dialogue** service. 
3. The **Assistant Dialogue** services analyzes the query and determines the **Actor** is trying to call a third-party skill. Continuing the example, the **Actor** invoked **Echo** with the query **hello**.
4. The **Assistant Dialogue** checks with the **Assistant skills** service to verify if this particular user has access to the **Echo** skill.
5. If the **Actor** has access to the given Skill, the request goes to the **Assistant skills** service for further processing. 
6. If the requested skill is not available for the **Actor**, then the request goes to **Assistant NLP** for handling instead.
7. The **Assistant skills** service encrypts and signs the request and sends it to the **Third-Party skill** service hosted by a third-party developer.
8. The **Third Party skill** service handles the request and produces a final response, which is then passed back via the same pipeline in reverse to the client.

## Developing a Skill

Developers can build and implement skills in any preferred programming language and web framework, as long as the proper security components are met, and requests from the **Assistant skills** service match the expected format.

The **Assistant skills** service communicates with **Third-Party skills** via secure HTTPS requests. Skills specify `directives` in order to make control the device response. The response payload also requires a `challenge`. View the Skills Reference guide for more information on [Assistant Directives](https://developer.webex.com/docs/webex-assistant-skills-reference-guide#assistant-directives), and the [Response Payload](https://developer.webex.com/docs/webex-assistant-skills-reference-guide#response-payload) structure.

In the [Assistant Skills SDK Guide](https://developer.webex.com/docs/webex-assistant-skills-guide), we will walk through developing an
Assistant skill using the Webex supported Python SDK, as well as showcase some of the tooling provided. It's important to note that the SDK does not need to be used, but it does have some support for starting and testing a skill.
