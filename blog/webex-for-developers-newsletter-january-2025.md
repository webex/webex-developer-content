---
type: Article
title: Webex for Developers Newsletter – January 2025
canonical_url: https://developer.webex.com/blog/webex-for-developers-newsletter-january-2025
content_type: blog
date: '2025-01-27'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/webex-for-developers-newsletter-january-2025)

Greetings and a very happy new year, Webex developers! There are a lot of exciting announcements and updates to share with you as we roll into 2025. So, let's get right to it and check out all the latest news!

### 🎤 Catch the Webex Developer Sessions at Cisco Live Amsterdam 2025

We are happy to announce the lineup of sessions for Webex developers at Cisco Live Amsterdam 2025. Whether you're looking to enhance your virtual meeting applications, dive into AI innovations, or explore the latest in Webex platform APIs, there's something for everyone. Get ready to engage with industry experts, participate in hands-on workshops, and expand your skills with our diverse range of sessions at #CiscoLiveEMEA.

[Read the blog →](https://developer.webex.com/blog/announcing-webex-developer-sessions-at-cisco-live-amsterdam-2025)

### 🔌 Using the New HTTP Connector for Webex Contact Center APIs

Webex Developer Evangelism Leader, Adam Weeks, recently published another blog that introduces a powerful new feature for Webex Contact Center: the ability to leverage Webex Contact Center (CC) APIs from within Flow Designer using a new Webex CC HTTP Connector. See how this new addition empowers organizations to seamlessly integrate public Webex CC APIs into the Webex Contact Center Flow Designer for creating powerful automated workflows.

[Read the blog →](https://developer.webex.com/blog/using-the-new-http-connector-for-webex-contact-center-apis)

### 🤖 How to Create Your Own RSS Feed Parser Bot for Webex

In another helpful post by Developer Support Engineer, Raffaele Lagana, learn how to deploy your very own RSS parser bot that runs in Webex. The blog covers a sample application you can start off with that has the ability to read RSS feeds and update a messaging space through a Webex Bot.

[Read the blog →](https://developer.webex.com/blog/how-to-create-your-own-rss-feed-parser-bot-for-webex)

### 🖥️ Webex Developer Public Webinars

On **Wednesday, February 26, 2025, at 1:00PM EST**, join us for our next public webinar where we'll demo the *Integrations Studio for Webex Connect*. The studio makes it easy to build, share and manage integrations that automate customer communication and customer experience workflows across various channels and regions at scale. See how you can bring your own functionality as well as third party APIs to Webex Connect's enterprise-grade flow builder to create repeatable, branded solutions exclusively for your customers, or market them on the Webex App Hub.

[Register for the live webinar →](https://evangelism.webex.com/weblink/register/rf7b608feefcdadff117ff9543ad18a22)

In case you can’t make the live event, you can always watch the session recording later or check out all the past sessions on our [webinars page](https://developer.webex.com/webinars).

### 🦾 Look, Ma, No Hands: Using AI to Generate and Refine Webex GitHub Sample Documentation

New APIs and features are frequently being added to the Webex Developer platform, which always means more work for the documentation team. This is another area where AI tools can help get the job done more quickly and efficiently. In an insightful blog post by Technical Documentation Leader, John Francis, shows us some of the ways that he's been integrating AI tools into his daily workflows, including creating cleaner GitHub pull requests descriptions, uncovering key marketing points for product teams, and simplifying the review process for new content submissions.

[Read the blog →](https://developer.webex.com/blog/look-ma-no-hands-using-ai-to-generate-and-refine-webex-github-sample-documentation)

### 👩🏽‍💻 Developer βeta: Webex Click-to-Call and Webex Developer AI Assistant

Currently, there are two features that are active for testing and providing feedback in the Developer βeta program:

- First is **Webex Click to Call**, a powerful new application type that is implemented through the Web Calling SDK. This can power use cases such as connect with a support desk or sales team at the click of a button, and the call happens right in the browser.
- The other beta feature is **AI Assistant for Webex Developers**, a chat interface powered by a large language model (LLM), accessible to all signed-in developers. Developers can provide a description of their intended project, and the assistant will handle the complex tasks, presenting relevant documentation, APIs, and suggested tools. Additionally, the assistant can generate code snippets to aid in building and deploying all kinds of Webex integrations.

[Join the βeta →](https://cs.co/webexdeveloperbeta)

### 🖱️📞 Using the Webex Click-To-Call Feature

To help developers hit the ground running with the “Webex Click to Call” beta feature, Adhwaith Menon from the Web SDK Engineering team published a marvelous quick start guide inside a blog post. The blog includes detailed step-by-step instructions for getting set up and a helpful Vidcast to show how everything comes together.

[Read the blog →](https://developer.webex.com/blog/power-your-customer-experience-using-the-webex-click-to-call-feature)

### 📝Webex API Recent Changelog Hits

There are also two important changes, among others, that were recently listed in the Webex API Changelog:

- **NEW**- January 13, 2025: Webhooks for Webex events are provided with a `X-Spark-Signature` when a [secret has been provided during webhook registration](https://developer.webex.com/docs/webhooks#handling-requests-from-webex). The signature corresponds to the `HMAC-SHA1` hash of the webhook payload. We now offer additional HMAC's namely `HMAC-SHA256` and `HMAC-SHA512`. These can be found in the new header `X-Webex-Signature`.
- **Breaking Change** - January 21, 2025: Starting on *March 2, 2025*, the `sharedLineIndex` field will be mandatory when `lineKeyType` is `SHARED_LINE` for the following APIs [Modify Device Layout by Device ID](https://developer.webex.com/docs/api/v1/device-call-settings/modify-device-layout-by-device-id), [Create a Line Key Template](https://developer.webex.com/docs/api/v1/device-call-settings/create-a-line-key-template), and [Modify a Line Key Template](https://developer.webex.com/docs/api/v1/device-call-settings/modify-a-line-key-template).

[Full Webex API Changelog →](https://developer.webex.com/docs/api/changelog)
