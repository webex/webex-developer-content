---
type: Article
title: Seamlessly Share Your Apps in Webex
canonical_url: https://developer.webex.com/blog/seamlessly-share-your-apps-in-webex
content_type: blog
date: '2023-05-24'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/seamlessly-share-your-apps-in-webex)

The Embedded Apps Framework supports “Open for All” which allows all meetings participants to collaborate over certain content as a whiteboard as an example. In some use cases, the initiator of the app might need to screen share the app to all meeting participants and thus provide them with read-only version of what is happening on his app. This is essential in industries as education, healthcare and more where in some use cases, collaboration over certain app content is not desired.

### Introducing setPresentationUrl

We have some exciting news for developers who are looking for a more seamless way to share their web applications within Webex. We are thrilled to announce the latest feature enhancement to the Webex Embedded Apps Framework, which now allows developers to screen share their app directly from within Webex, without having to open an external browser.

With this new feature, you can now offer a more efficient and streamlined user experience to your end-users. Whether you're collaborating with your team, holding online meetings, or delivering a webinar, the ability to share your web app within Webex can significantly enhance the overall experience.

### Using setPresentationUrl

To use this feature, you need to create an embedded app on the Webex Developer Portal. Once you create the embedded app, add the Webex Embedded App SDK to your app and call the new [setPresentationUrl](https://developer.webex.com/docs/embedded-apps-api-reference#Meeting+setPresentationUrl) method to allow your users to see a live view of your entire web browser within the Webex environment, without having to navigate to an external browser.

Here's how you can enable this feature in your embedded app:

1. Create an embedded app on the Webex Developer Portal.
1. Add the Webex Embedded App SDK to your application.
1. Configure the embedded app to use the Webex SDK to share your web browser within Webex.
1. Your users will now be able to share your app directly within Webex, without having to leave the environment.

This feature is particularly useful for developers who want to offer a more seamless and integrated experience. Whether you're developing a productivity app or a customer support tool, the ability to share your entire web browser directly within Webex can help enhance the overall user experience and streamline collaboration.

The latest feature enhancement to the Webex Embedded Apps Framework offers a new and exciting way for app developers to share their web app within Webex. By creating an embedded app and using the new SDK method, you can enable your end-users to view your web app directly within the Webex environment, without having to navigate to an external browser. This can help streamline collaboration and enhance the overall user experience. So what are you waiting for? Create your embedded app on the Webex Developer Portal today and experience the benefits for yourself!

If you have any questions or interested to provide feedback on the sidebar apps, please reach out to our [developer support team](https://developer.webex.com/support).
