---
type: Article
title: Webex for Developers Newsletter – February 2025
canonical_url: https://developer.webex.com/blog/webex-for-developers-newsletter-february-2025
content_type: blog
date: '2025-02-24'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/webex-for-developers-newsletter-february-2025)

Greetings, Webex developers! It has been another eventful month for our community that produced some newsworthy items. Check out all the latest updates and announcements right here.

### 👩🏽‍💻 Developer βeta: Webex Click-to-Call and Webex Developer AI Assistant

Attention early adopters! We have some new features in the Developer βeta program that you can go check out.

- First is **Webex Click to Call**, which is designed to provide a user-friendly calling experience for guest users to call people within your organization. This powerful feature eliminates the need for downloads, accounts, and authentication, to ensure customers can connect with your enterprise effortlessly with just click of a button, improving overall customer satisfaction and engagement.
- Next is **AI Assistant for Webex Developers**, which is a chat interface powered by a large language model (LLM) to assist users to find the right Webex developer tools and code generation for their projects. Developers can either click through options or provide a plain text description of their intended project, and the assistant will handle the complex tasks, presenting relevant documentation and appropriate tools like APIs and SDKs. Additionally, the assistant can generate code snippets to aid in building integrations, thus enabling even customer administrators to create their own integrations.
- Finally, coming very soon to the beta program is a preview of the **Converged Webex Developer Portal**, which combines resources for both the Webex Suite and Webex Contact Center platforms. Today, we have two different portals for Contact Center and Webex Suite. This poses a challenge for a developer who is interested in developing an application/integration for Webex Suite and Webex Contact center as the documentation and APIs are available in two different portals. Having all the contents available in single portal will assist the developers to easily discover the contents.

Don't miss out on testing these new features early!

[Join the βeta →](https://cs.co/webexdeveloperbeta)

### 🖥️ Webex Developer Public Webinars

On **Wednesday, February 26, 2025, at 1:00PM EST**, join us for our next public webinar where we'll demo the *Integrations Studio for Webex Connect*. The studio makes it easy to build, share and manage integrations that automate customer communication and customer experience workflows across various channels and regions at scale. See how you can bring your own functionality as well as third party APIs to Webex Connect's enterprise-grade flow builder to create repeatable, branded solutions exclusively for your customers, or market them on the Webex App Hub.

Register for the live session or watch any of our previous webinar recordings on-demand later from our webinars page.

[Attend or watch webinars →](https://developer.webex.com/webinars)

### 👩🏻‍🔧 What's New for Webex Contact Center Administrators

There are several new updates for Webex Contact Center that were recently announced. Here are some of the highlights:

- **Programmatic Flow Management with the List and Publish APIs**
  - These new APIs supplement the existing Import and Export APIs for flows and subflows, enabling the full automation of flow management for both new and migrating organizations. This update allows developers and partners to list, export, import, and publish flows and subflows programmatically between organizations, eliminating manual steps and thus enhancing efficiency in managing many flows and subflows.
- **Self-Service SMS (10DLC) and WhatsApp numbers**
  - United States customers can now request phone numbers, including 10DLC, directly through the Webex Connect as a self-service feature.
- **Cisco AI Assistant for Contact Center**
  - Get ready to transform your contact center operations and delight your customers with Cisco AI Assistant for Contact Center! AI Assistant revolutionizes customer service by enhancing your efficiency and elevating customer satisfaction with AI-generated call summaries, AI-powered Agent Wellbeing, Auto CSAT, and Topic Analytics.
- **Enhanced Zendesk Integration**
  - Agent productivity and customer support is now more streamlined and boosted with exciting new enhancements to our Zendesk Connector! Agents can now create Zendesk tickets and new customer tickets directly from Agent Desktop. They can also automatically populate ticket fields and link them to various contacts.

[Learn more →](https://help.webex.com/en-us/article/nv7abhz/What's-new-for-administrators-in-Webex-Contact-Center)

### 📝Webex API Recent Changelog Hits

We also have some important API updates recently listed in the Webex API Changelog:

- **NEW**– February 6, 2025: Descriptions of the following fields have been added to [Get Detailed Call History](https://developer.webex.com/docs/api/v1/reports-detailed-call-history/): Caller ID number, External caller ID number, Redirecting party UUID, Device owner UUID, Call Recording Platform Name, Call Recording Result, Call Recording Trigger, and Public Calling IP Address.
- **NEW** – February 11, 2025: As a host or cohost of a meeting, you can invite a SIP participant to join the meeting via the [Call Out a SIP Participant API](https://developer.webex.com/docs/api/v1/meeting-participants/call-out-a-sip-participant). You can also cancel the call to a SIP participant before the ringing on the invited SIP device stops via the [Cancel Calling Out a SIP Participant API](https://developer.webex.com/docs/api/v1/meeting-participants/cancel-calling-out-a-sip-participant).
- **NEW** – February 14, 2025: As a meeting host, you can set up live streaming for a meeting with the `enabledLiveStream` and `liveStream` attributes when the meeting is created using the [Create a Meeting API](https://developer.webex.com/docs/api/v1/meetings/create-a-meeting). When the meeting is started, the meeting host can start the live streaming by selecting the three dots, choosing **Start live streaming** and then **Go live** from the meeting client. The live streaming is started for the meeting without any ad-hoc configuration required. Live streaming can also be enabled for an existing meeting using [Patch a Meeting](https://developer.webex.com/docs/api/v1/meetings/patch-a-meeting) or [Update a Meeting](https://developer.webex.com/docs/api/v1/meetings/update-a-meeting) with the `enabledLiveStream` and `liveStream` attributes.

[Full Webex API Changelog →](https://developer.webex.com/docs/api/changelog)
