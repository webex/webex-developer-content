---
type: Article
title: Webex for Developers Newsletter – September 2025
canonical_url: https://developer.webex.com/blog/webex-for-developers-newsletter-september-2025
content_type: blog
date: '2025-09-22'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/webex-for-developers-newsletter-september-2025)

Greetings, Webex developers! We have another round of new content and events for you to discover this month. Read on to get all the latest updates and community announcements for the full Webex Developer ecosystem.

### 📺 Public Developer Webinar: Discover and Build with Webex Service Apps

On Wednesday, October 22<sup>nd</sup> at 1:00PM EDT, join our next public webinar to simplify your Webex API development and resolve common issues more effectively. We will explore the newly published [Webex API Troubleshooting Guide](https://developer.webex.com/docs/troubleshooting), offering developers practical strategies to quickly diagnose and fix problems. This session will cover how to understand error codes, troubleshoot API request failures, authorization, and rate limiting issues. We will also go over best practices for preventing issues and using essential tools for quicker solutions. Whether you're a new or experienced Webex developer, this webinar will help you build more reliable integrations with confidence. Register now to become a Webex API troubleshooting expert!

If you can’t make it to the live session, no problem! You can watch all our previous webinar recordings on-demand, including the most recent one, **Building with the Webex Mobile SDK - Introduction and Key Flavors**, right on our webinars page. Come and explore our growing library!

[Attend or watch webinars →](https://developer.webex.com/webinars)

### 🧑🏽‍🔧 Using WebSockets with the Webex JavaScript SDK

In an updated blog post by Dev Support Engineering Leader, Janos Benyovszki, learn how to leverage WebSockets in the Webex JavaScript SDK to maintain persistent connections and allow direct communication with the Webex API. This approach can also be an effective solution if your app needs to run behind a corporate firewall or in restrictive environments. In this blog, Janos walks us through creating and using WebSockets with the SDK to listen for events sent from Webex, and have your application react accordingly.

[Read the blog →](https://developer.webex.com/blog/using-websockets-with-the-webex-javascript-sdk)

### 🏋️‍♀️ Webex Academy Training Program at WebexOne 2025 in San Diego

Register for WebexOne 2025 in San Diego that takes places on SEP 28 - OCT 1 and join the Webex Academy Training Program! With the Conference Pass + Training ticket, you get access to 4 days of in-person technical training classes and hands-on labs, plus Cisco Continuing Education credits for your participation. After the event, you’ll also get exclusive access to all the classes on-demand.

Get a 50% discount with promo code: **WX1ACADEMY50**

[Register today →](https://www.webexone.com/training.html)

### 👩🏽‍💻 Now in the Developer βeta Program - Webex Contact Center Widgets

Simplify your contact center integration with Webex Contact Center Widgets—a collection of ready-to-use, modular components designed to seamlessly bring contact center functionalities into any third-party web application. These widgets eliminate the need for customers to build and manage their own UI components or handle the complexities of API interactions and business logic, letting you focus on delivering exceptional user experiences. Join the public beta to get early access today!

[Join the βeta →](https://cs.co/webexdeveloperbeta)

### 🗝️ Service Apps Token Management: A Developer's Guide to Automation

Devices in the Cisco Desk Phone 9800 Series have very flexible administration capabilities via the Webex Calling APIs, to automate lifecycle management, customization, and post-activation configurations on devices. In a new blog, Senior Developer Evangelist, Phil Bellanti, highlights some key distinctions between Cisco 9800-series phones and Cisco MPP devices, to clarify some of the notable differences in how they are respectively set up and managed. Phil also goes through all the Webex APIs for the 9800 Series and groups them into specific feature categories for easier understanding and usage.

[Read the blog →](https://developer.webex.com/blog/service-app-token-management-a-developer-s-guide-to-automation)

### 📝 Webex API Recent Changelog Hits

Highlighting some important updates recently listed in the Webex API Changelogs:

- **UPDATED IN WEBEX CONTACT CENTER–** September 10, 2025: We have added a new field `alg` to the public key schema used in the Bring Your Own Device Service BYODS framework. This is an additive change that maintains backward compatibility.
  - **Added Field:** `alg` - Algorithm identifier for the public key
  - **Location:** Public key objects within the BYODS framework
  - **Type:** String (expected values may include standard algorithm identifiers like "RS256", "ES256", etc.)

[Full Webex Contact Center API Changelog →](https://developer.webex.com/webex-contact-center/docs/api/changelog/webex-contact-center) 

- **WARNING FOR THE WEBEX APIs**– September 8, 2025: We've implemented stricter validation for API request headers. If your API calls suddenly stop working and you haven't made any changes on your end, please double-check your headers for correctness. Requests with incorrect or missing headers will now be rejected.

- **BREAKING CHANGE FOR THE WEBEX APIs**– September 10, 2025: We will follow a stricter implementation for the JWT guest token to follow the standards more closely. Previously a string was accepted in the exp field to indicate when the token expires. We are changing this field to allow an Integer only and this change will be enforced *Nov 1, 2025*. You can make the change right now as today both string and int will be accepted.

[Full Webex API Changelog →](https://developer.webex.com/admin/docs/api/changelog/webex-admin)
