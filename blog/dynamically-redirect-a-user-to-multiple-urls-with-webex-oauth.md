---
type: Article
title: Dynamically Redirect a User to Multiple URLs with Webex OAuth
canonical_url: https://developer.webex.com/blog/dynamically-redirect-a-user-to-multiple-urls-with-webex-oauth
content_type: blog
date: '2023-11-01'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/dynamically-redirect-a-user-to-multiple-urls-with-webex-oauth)

In an era where user experience is paramount, the ability to dynamically redirect users to different URLs based on their preferences, behavior, or device type can be a game-changer. This powerful strategy not only enhances the user journey but also provides valuable data for optimization. Additionally, it offers the added benefit of managing multiple redirect URLs without the need for constant visits to the Webex Developer Portal.

In this blog, we'll dive into the technical details of how to implement dynamic redirection using Webex OAuth and explore important guidelines to keep your apps secure. Whether your goal is to refine your offerings through A/B testing, personalize the user experience, or ensure seamless multi-platform support, this guide is your key to mastering this essential technique. Let's get started!

The ability to dynamically redirect users to different URLs can offer significant benefits for your Webex application. Here are some practical scenarios:

- A/B Testing: Dynamically redirect users to different versions of a web page or app feature to gather valuable data on user preferences and behaviors. This can help in refining and optimizing your offerings.
- Personalized User Experience: Tailor the user journey by redirecting users to URLs that match their behaviors and preferences. Personalization can lead to higher user engagement and satisfaction.
- Multi-Platform Support: In the era of multi-platform usage, ensure a seamless user experience by redirecting users to platform-specific URLs (web, mobile, etc.) based on their device.

One significant advantage of this approach is the ability to add multiple redirect URLs without needing to visit the Webex Developer Portal each time you want to add a new redirect URI.

### Technical Details

When registering a Webex OAuth client app that uses the authorization code flow (3-legged OAuth), incorporate a state parameter to your authorization URL to enable dynamic redirection. Here's an example:

`https://webexapis.com/v1/authorize?client_id=yourclientid&response_type=code&redirect_uri=http%3A%2F%2Fyourapp.com%2Foauth&scope=spark%3Arooms_read&state=AnyValue`

After the user completes the authorization code flow, Webex will return the state query parameter value in your redirect URL:

`GET http://yourapp.com/oauth?code=yourauthorizationcode&state=AnyValue`

To pass a URL with the state parameter, URL-encode it as follows:

`https://webexapis.com/v1/authorize?client_id=yourclientid&response_type=code&redirect_uri=http%3A%2F%2Fyourapp.com%2Foauth&scope=spark%3Arooms_read&state=https%3A%2F%2Fanothersite.com`

When Webex redirects the user to your app, use the state parameter value to redirect them to another destination.

### Guidelines

Make sure you adhere to the following guidelines:

- **Do Not Expose the Authorization Code**: Avoid revealing the OAuth authorization code by redirecting the user to another trusted page in your app before redirecting them to an untrusted site.
- **Do Not Append Query Parameters to the Redirect URI**: Although Webex currently supports query parameters in the redirect URI, it's recommended to use the state parameter for redirection.

By effectively implementing the OAuth protocol and harnessing the power of dynamic redirection, you can not only secure your Webex apps but also enhance the user experience, gather valuable data, and ensure a seamless user journey across multiple platforms without the need to constantly visit the Webex Developer Portal.

### Test It Out

Want to see all this functionality without building an app of your own first? You can with our [Webex OAuth Code Grant Flow Demo](https://webexsamples.github.io/webex-auth-sample/webex-auth.html). Simply create your integration on the [Developer Portal](https://developer.webex.com/my-apps) and use `https://webexsamples.github.io/webex-auth-sample/webex-auth.html` as a redirect URI. Once that is created, you can see how the state parameter is passed back and forth during the Code Grant Flow. The code for the sample demo app can be found on our GitHub at https://github.com/WebexSamples/webex-auth-sample.

### Need Some Help? We Got You Covered!

We are excited to provide you with support for these features. If you need help, the [Webex Developer Support Team](https://developer.webex.com/support) is standing by and happy to assist. You can also start or join a conversation on the [Webex for Developers Community Forum](https://cs.co/WebexDeveloperCommunity).
