---
type: Article
title: Using OAuth with Webex in Your React Application
canonical_url: https://developer.webex.com/blog/using-oauth-with-webex-in-your-react-application
content_type: blog
date: '2021-12-06'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/using-oauth-with-webex-in-your-react-application)

Here on the Webex Evangelism team, we spend a lot of time spinning up samples and test apps to try out all the new and exciting features from the Webex team. Every time we did, we found ourselves writing a lot of the same authorization code to start the project. We decided to build a quick sample React application that does only the implicit grant flow to help us to focus on the APIs we are testing instead of dealing with authentication. We hope this OAuth sample can help you bootstrap your next React project!

[https://github.com/WebexSamples/webex-react-oauth-sample](https://github.com/WebexSamples/webex-react-oauth-sample)

When building a web application with React that works with our Webex APIs, one of the first things you build is the authentication. Webex APIs allow you to interact with Webex services on behalf of a Webex user. To utilize Webex APIs, you must have an access token from the user passed with your API request. This token is obtained by using a Webex Integration to start the OAuth flow.

We will be utilizing the OAuth implicit grant flow for this example. The implicit grant flow is a less secure flow than some of the other flows because all the token management is handled on the client side, but it allows you to quickly get a front-end application running without a server component. The Webex OAuth implicit grant flow is as follows:

- Web App sends the user to the [https://webexapis.com/v1/authorize](https://webexapis.com/v1/authorize) endpoint to authorize.
- Webex User logs into Webex and grants Web App access to Webex User’s account.
- Webex Authorization endpoint redirects user back to Web App and includes the user’s token in the URL’s query parameters.
- Web App parses token from query parameters and uses it in Webex API requests

&nbsp;

### Hooks

In our sample application, we’ve created two different React hooks to assist with the OAuth implicit grant flow: “useWebexOAuth” and “useCurrentUri”.

#### “useCurrentUri”

[useCurrentUri](https://github.com/WebexSamples/webex-react-oauth-sample/blob/main/src/useCurrentUri.js) is a hook that gets the current URL and encodes it for use as a redirect URI. The redirect URI is where we tell the Webex authorization flow to return to. The goodness behind this hook is that you can use this hook in all your environments without having to hard code URIs.

#### “useWebexOAuth”

[useWebexOAuth](https://github.com/WebexSamples/webex-react-oauth-sample/blob/main/src/useWebexOAuth.js) captures the access token from the “access_token” URL hash parameter that returns after the implicit grant flow succeeds, stores it in a React state, then clears the hash parameter for added security.

&nbsp;

### What’s Next?

Taking this application as a starter, we are hoping to have more focused and direct sample applications in our [Webex Samples organization on Github](https://github.com/WebexSamples). We’re excited to see what you’ll build!

Be sure to reach out to our [developer support team](https://developer.webex.com/support) for any help or requests you need!
