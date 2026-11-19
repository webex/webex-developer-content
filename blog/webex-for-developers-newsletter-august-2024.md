---
type: Article
title: Webex for Developers Newsletter – August 2024
canonical_url: https://developer.webex.com/blog/webex-for-developers-newsletter-august-2024
content_type: blog
date: '2024-08-26'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/webex-for-developers-newsletter-august-2024)

Greetings, Webex Developers! Great things are happening this month, as we have a slew of new content on both the Webex and Webex Contact Center platforms to learn more about. Keep reading to get all of the exciting details.

### 🛠️Build a Webex Connect Flow: Step by Step Guide

In a [new blog post](https://developer.webex.com/blog/build-your-first-webex-connect-flow-a-step-by-step-guide) on the CPaaS side, Product Marketing Manager, Sam Watson shows us how we can work quicker and smarter by using the Flow Builder, which is a tool for building, configuring, deploying, and iterating workflows that automate communication processes across a customer journey in [Webex Connect.](https://cpaas.webex.com/products/webex-connect) He takes us step-by-step to create, test, and troubleshoot a Webex Connect flow, complete with screenshots and easy to follow instructions. It has never been easier to get started!

### 🧑‍💻Rapidly Adapt Your CX Workflows with Webex Contact Center Flow Designer

In another [blog post](https://developer.webex.com/blog/rapidly-adapt-your-cx-workflows-with-webex-contact-center-flow-designer) published recently, Engineering Product Manager, Arunabh Bhattacharjee, covers all the recent updates on the Webex Contact Center Flow Designer platform. There are several new features to learn about, such as Flow Versioning, Percentage Allocation of Flow Traffic, Sub-flows and Dynamic Variable Support. Find out how these new features enable enterprise-grade CX change management for rapid and risk-free innovation.

### ⚙️Leveraging the Agent Desktop SDK to Build Custom Widgets in Webex Contact Center

In the [next entry](https://developer.webex.com/blog/leveraging-the-webex-contact-center-agent-desktop-sdk-in-your-custom-widgets) in our Contact Center Custom Widgets blog series, Adam Weeks goes over the key features of the Desktop SDK. This is ideal for developers looking to build robust and interactive web apps within the Agent and Supervisor Desktop. Adam shows developers how to get started and provides a code tour of a handy sample app. You will learn how to manage agent states, handle interactions, and real-time data &amp; event handling.

### 📺New! Webex for Developers Content on YouTube

You can find *Webex for Developers* videos on YouTube! We're thrilled to announce the new [Webex for Developers YouTube playlist](https://www.youtube.com/playlist?list=PL2k86RlAekM_bIUrvVw4Haq_0xxTez9zU), as part of Cisco DevNet channel. There is already a variety of content available to watch there, including developer how-to videos, product announcements, and recordings of our previous [developer webinars](https://developer.webex.com/webinars). Go check out the playlist today!

### 🖥️Webex Developer Public Webinars

Join the Webex Developer Evangelism team on Wednesday, September 25 at 1:00PM EDT, for our next public webinar: **AI and Webex: Transforming Industries with Cutting-Edge Integrations**. Discover how AI and Webex are revolutionizing healthcare, finance, retail, and manufacturing industries, and see some real-world integrations and innovative applications in action. [Register for the live event today](https://evangelism.webex.com/weblink/register/r0d92a7f2591bb07c38dbda71ec830354)!

Otherwise, if you can’t make the live event, watch the session recording later or check out other past events over on our [webinars page](https://developer.webex.com/webinars).

### 🧪Webex Developer βeta Program Activity

The Webex Developer Beta Program lets you take a sneak peek and test out our upcoming features before they are released. We currently have two active beta features you can try out and provide feedback on now:

- Webex Space Widgets via CDN Beta
- Webex Meeting Widgets via NPM Beta

Now is your chance to become a Webex “early-adopter” developer! To get started, head over to the [Developer Beta Program information page](https://gobeta.webex.com/key/dev-platform).

### 🗓️Webex Contact Center API: Recent Updates

**As noted in the [API changelog](https://developer.webex.com/docs/api/changelog) on August 14, 2024:** We have updated the base URLs for the CJDS APIs across several environments:

- UL - `https://api.wxcc-us1.cisco.com`
- EU1 - `https://api.wxcc-eu1.cisco.com`
- EU2 - `https://api.wxcc-eu2.cisco.com`

If you are using any previous URLs, please re-enable the Webex Contact Center connector as outlined on the [Getting Started page](https://developer.webex.com/webex-contact-center/docs/journey-getting-started) to ensure you continue receiving contact center events for the journey widget.

### 📒Webex Platform API Changelog Highlights

August has several entries in [Webex API Changelog](https://developer.webex.com/docs/api/changelog) and we always recommend checking this page frequently to stay up to date. Here are some latest items you can find there:

- **August 23, 2024 - NEW:** As an administrator, you can reassign a list of call recordings or all call recordings of a particular user to a new user through the [Reassign Recording](https://developer.webex.com/docs/api/v1/converged-recordings/reassign-recordings) endpoint.
- **August 21, 2024 – NEW:** Service numbers are now supported for Premises-based PSTN. These are local telephone numbers considered as high utilization or concurrent, making them ideal for assignment to high-volume services such as Auto Attendants, Hunt Groups, and Call Queues. The [Add Numbers](https://developer.webex.com/docs/api/v1/numbers/add-phone-numbers-to-a-location), [Get Numbers](https://developer.webex.com/docs/api/v1/numbers/get-phone-numbers-for-an-organization-with-given-criterias), and [Initiate Number Jobs](https://developer.webex.com/docs/api/v1/numbers/initiate-number-jobs) APIs are modified to support service numbers. Additionally, feature-specific available numbers APIs such as [Hunt Group](https://developer.webex.com/docs/api/v1/features-hunt-group/get-hunt-group-primary-available-phone-numbers), [Location](https://developer.webex.com/docs/api/v1/location-call-settings/get-location-call-intercept-available-phone-numbers), [Person](https://developer.webex.com/docs/api/v1/user-call-settings/get-person-primary-available-phone-numbers), and [Workspace](https://developer.webex.com/docs/api/v1/workspace-call-settings/get-workspace-fax-message-available-phone-numbers) have been added to help identify numbers that can be associated with specific members or features. These feature-specific APIs are streamlined with fewer parameters, making them more easily to use as alternatives to the more general [Get Numbers](https://developer.webex.com/docs/api/v1/numbers/get-phone-numbers-for-an-organization-with-given-criterias) API.
- **August 21, 2024 – NEW:** A new webhook resource allows you to receive notifications for status changes of admin batch jobs, reducing the need for manual status checks. For setup instructions and more details, see [Webhooks Reference Page](https://developer.webex.com/docs/api/v1/webhooks).
