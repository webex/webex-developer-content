---
type: Excerpt
canonical_url: https://developer.webex.com/docs/introduction-to-webex-apps
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Types of Webex Applications
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/introduction-to-webex-apps). [Full Markdown](../../../../docs/introduction-to-webex-apps.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites](001-prerequisites.md)

## Article introduction

This tutorial provides an introduction to Webex's extensibility.

---

In this introduction to the Webex REST API, you will use the interactive documentation to experience Webex programmability. The tutorial will then go through a few use-cases, and drill into the fundamentals of Webex Apps.

## Selected section

## Types of Webex Applications

In previous steps, we covered how Webex REST API makes it simple to create automated interactions against the Cisco Webex Cloud Platform.

Here are various types of applications you could build using the same approach:

- **Controller**: This type of app listens for events in Webex, such as new messages that contain a specific mention, or a participant being added to a space. When these events happen, the app could send an SMS alert or use Webex to send data to an enterprise back-end.

    

> **Info**
>
> *NOTE*: In Webex terminology, an app that listens but does not take any action is called a *watcher*.



- **Notifier**: This type of app responds to events by sending messages to a Webex space. For example, it could send a message to a "Business Activity" space when new customers sign-in and orders are created or canceled. Employees would monitor new messages in the “Business Activity” space and respond if further actions were needed.

- **Interactive Assistants**: This type of app asks a customer a set of questions and uses the answers to perform actions such as filling out a form, scheduling an appointment, or simulating the interest on loan. These types of interactive apps are sometimes called "chat bots" or simply "bots."

When extending Webex, one uses the term *applications* rather than the generic *bots*. As you'll see in next chapter, the concept of a "Webex Bot" is associated with *bot accounts* and specific behaviors attached to 'Direct' and 'Group' spaces.

### Create your application

Depending on your technical background and business goals, there are several ways you can go about creating an application:

- You can design and build an app using a visual integration tool. This approach is like creating software from Lego-like building blocks and requires little to no coding. These blocks perform defined tasks and connect to various back-end services.

    Various third-party vendors also offer visual integration tools and services, such as IFTTT, Zapier, Built.io, Gupshup, Stamplay, Workato. These services simplify deploying applications and offer benefits such as pre-configured integrations, natural language processing, voice synthesis, voice recognition, and image analysis.

- You can write and deploy your code. The Webex API enables you to create an application in any language, and the community has been working on frameworks and examples to help you on this journey.

    Delivering apps that are more than prototypes requires allocating effort and resources to meet availability and security requirements. These include setting up and  monitoring a DNS, load-balancing, firewalls, traffic monitoring, rate limitations, etc.

In the upcoming Tutorials, you’ll have an opportunity to create apps using code or third-party tools.
