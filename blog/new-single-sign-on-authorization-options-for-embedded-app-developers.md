---
type: Article
title: New Single Sign-On Authorization Options for Embedded App Developers
canonical_url: https://developer.webex.com/blog/new-single-sign-on-authorization-options-for-embedded-app-developers
content_type: blog
date: '2023-09-14'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/new-single-sign-on-authorization-options-for-embedded-app-developers)

Scrawled on sticky notes stuck to monitors or under keyboards. Forced changes every 90 days. Millions of dollars’ worth of IT admin time in reset flows. Recycled, on average, 13 times. For all the effort we put into protecting our passwords, however misguided these efforts sometimes are, stolen passwords still account for 80 percent of all hacking-related breaches and employees still manage dozens of them – spending collectively hundreds of thousands of hours logging in, looking up, resetting, getting locked out and starting all over again.

Single sign-on (SSO) takes aim at these problems, simplifying password management and leveraging the trusted security infrastructures of others. As a time-saver and an insurance policy for an organization, it’s a no-brainer.

Webex has announced a new feature on the Embedded App Framework that focuses on strengthening security, reducing time-wasting cycles of password resets, and taking a common stressor out of the employee experience.

The new feature allows Webex Embedded App users to login into their Webex Embedded App account using their existing social media or Webex accounts rather than having to create a whole new password, streamlining login, and reducing the likelihood of forgotten passwords.

### Why Should Developers Use SSO

For Webex Embedded App developers, this means their apps can utilize existing single sign-on functionality for authenticating users. There are several reasons why a developer might choose to implement single sign-on (SSO) instead of building their own authentication system. Some of the key benefits of using SSO include:

- **Improved user experience**: With SSO, users only need to remember one set of login credentials (i.e. their SSO username and password) to access multiple applications. This makes it easier for users to access the applications they need, and it reduces the number of times they need to enter their login credentials.
- **Enhanced security**: SSO systems typically use strong authentication methods, such as two-factor authentication or biometric authentication, to verify the user's identity. This can help prevent unauthorized access to the applications that are protected by SSO. Additionally, SSO systems often use encryption to protect the user's login credentials as they are transmitted across the network.
- **Improved resource management**: Building and maintaining a custom authentication system can be a time-consuming and resource-intensive process. By using SSO, developers can offload the authentication process to a third-party service, which can save them time and resources that can be spent on other aspects of their application.
- **Easier integration with other applications**: Many applications and services support SSO, which means that developers can easily integrate their applications with SSO and allow their users to use their SSO credentials to access the application. This can make it easier for developers to add authentication to their applications and improve the user experience.

Overall, implementing SSO can provide many benefits for both developers and users, and it can be a more efficient and secure alternative to building a custom authentication system.

### Implementing SSO in Webex Embedded Apps

The Embedded Apps SDK has two different SSO options: third-party single sign-on and “Login with Webex”. If you are looking for an easy way to authenticate Webex users in your app without having to worry if [PII is enabled](https://developer-portal-intb.ciscospark.com/docs/embedded-apps-guide#personally-identifiable-information-pii-and-embedded-apps), utilizing “Login with Webex” is the route you will want to take. If your app users use a different third-party service for authentication, the new `initiateSystemBrowserOAuth()` function would be where you would start. Both methods have example code in our [open-source kitchen sink app](https://github.com/webex/EmbeddedAppKitchenSink).

#### Login with Webex

[Login with Webex](https://developer.webex.com/docs/login-with-webex) is the name of the OpenID Connect standard for using an existing Webex account for authentication. Following this flow will allow you to get details about the Webex user using your app from within Webex. By creating a Login with Webex integration, your app user will be taken through an OAuth flow within the Webex ecosystem and will result in your app receiving their user information. Stay tuned because a streamlined authentication flow is on the way for Webex users!

#### Third-Party Single Sign-On Support

Ensuring full support and safety for your users, Webex has provided a new function that opens the SSO flow in your users’ system browsers. In 2021, [Google removed support](https://developers.googleblog.com/2021/06/upcoming-security-changes-to-googles-oauth-2.0-authorization-endpoint.html) for embedded browser OAuth flows due to security concerns and we expect more to follow. The function your app will call to open this flow is the appropriately named `initiateSystemBrowserOAuth()`. Follow along on our [detailed docs](https://developer-portal-intb.ciscospark.com/docs/embedded-apps-guide#thirdparty-single-signon-sso-support) for guidance on how to use the function. You can also see an example implementation in our [open-source kitchen sink app](https://github.com/webex/EmbeddedAppKitchenSink).

### Wrapping Up

Webex's new SSO features are a valuable tool for app developers looking to improve their security posture and reduce the time and resources spent on password management. In addition to reducing password reset times and improving security, SSO also makes it easier for employees to access their accounts from any device or location. As more and more enterprises adopt collaboration solutions like Webex, SSO will become an increasingly important tool for managing user access and security.

Don’t forget that the [Webex Developer Support Team](https://developer-portal-intb.ciscospark.com/support) is standing by to assist. On top of that, anyone can ask a question, start a conversation, or join an existing discussion on the [Webex for Developers Community Forum](https://cs.co/WebexDeveloperCommunity). Follow along on Twitter via [@WebexDevs](https://twitter.com/WebexDevs) for updates and announcements.
