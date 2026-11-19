---
type: Article
title: Build your Webex Sidebar app to unlock productivity, CRM, and AI use cases for individual users!
canonical_url: https://developer.webex.com/blog/webex-sidebar-apps
content_type: blog
date: '2023-06-13'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/webex-sidebar-apps)

Today, Developers can build embedded apps that live inside the meetings and spaces contexts. This allows end users to get an immersive experience and reduce the context switching while using these apps directly in the Webex app and thus enhance the collaboration experience among meetings and spaces participants. However, in some use cases an app needs to be available outside the meetings and spaces for individual use by the end users to allow customers to satisfy several use cases as follows:

- Customer relationship management (CRM) Apps - For sales agents and customer service representatives in different domains as customer service, insurance and more, to access customers’ profile data for better assistance
- AI Apps– Virtual assistant that helps organization users with searching resources, editing documents, and providing relevant suggestions.
- Productivity enhancement apps – Note taking, To-do list and schedule management apps that can help users with enhancing their day-to-day productivity.
- Human Resources Apps – Directory and training apps that allow users to access their organization’s directory, trainings material and essential resources.
- Healthcare Apps – Apps that connect a user with healthcare providers.
- Wellness Apps – As apps tracking mental wellbeing of users, measure workplace satisfaction levels.

With the previous use cases in mind, the embedded apps framework has been expanded to allow developers to build Sidebar apps. These apps reside on the navigation panel/sidebar of the Webex’s application outside of the meetings and spaces.

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt68b456e1e13972d0/6462559060b10c490eaf9c19/sidebar-apps-blog-2.png)

Developers can also configure these applications to always be running, so that when you launch the Webex App. These apps will run in the background automatically. The background app's can also be developed to listen to incoming call events, extract caller's information, and get updates on the call lifecycle. This can be beneficial for CRM use cases where caller's profiles can be loaded before an agent/end user accepts an incoming call

Finally, to ensure organization administrators are in control, administrators will be able to decide which app will be enabled and allowed to be present on the Sidebar of the Webex app and assign it to the whole organization or certain user groups.

### Getting Started

Here's how you can build a sidebar embedded app:

1. Follow the instructions [here](https://developer.webex.com/docs/embedded-apps-guide#creating-an-embedded-app-in-the-developer-portal) to create an embedded app on the [Webex Developer Portal](https://developer.webex.com/) and use the new “Sidebar” context. Also, decide if your app will be used for call monitoring use cases or not so that you enable it to be always ON. Please note that only 3 always ON apps are allowed per organization.
2. Add the Webex Embedded App SDK to your application.
3. Submit your app for approval either to Webex if it’s a public app, or to the organization’s administrator if it’s a private app.
4. The organization users who will use this app, will now be able to find the app on the Webex’s app sidebar if the organization’s administrator has approved and allowed the app to be shown there.

The latest feature enhancement to the Webex Embedded Apps Framework offers a new and exciting way for app developers to build sidebar apps for further expansion of the supported use cases. So, what are you waiting for? Create your embedded app on the Webex Developer Portal today and experience the benefits for yourself!

Please take a look at our [developer guide](https://developer.webex.com/docs/embedded-apps-framework-sidebar-api-quick-start), to learn how to start using the new APIs for sidebar apps. If you have any questions or interested to provide feedback on the sidebar apps, please reach out to our [developer support team](https://developer.webex.com/support).
