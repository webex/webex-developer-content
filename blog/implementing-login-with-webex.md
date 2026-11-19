---
type: Article
title: Implementing Login with Webex
canonical_url: https://developer.webex.com/blog/implementing-login-with-webex
content_type: blog
date: '2022-09-13'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/implementing-login-with-webex)

The Webex Platform recently introduced the ability for developers to utilize a Webex user’s identity to authenticate with an external platform via the OpenID Connect Standard. In this blog, we dive into the ways an external Developer can implement the “Login with Webex” flows.

### Approaches

When building an authentication system, Developers need to take into consideration the scope and deployment of their existing application and choose the proper approach. The two approaches we are going to investigate in this blog are the use of the Implicit Grant Flow with an `id_token` response type and the Authorization Code Flow with PKCE.

Front End Developers whose applications live solely in the browser (commonly referred to as “Single Page Applications”) will rely on the Implicit Grant Flow. This allows the Developer to get the necessary information about the Webex identity without the need for any back-end storage or servers.

Full Stack Developers whose applications run on a server with some sort of storage mechanism can use the Authorization Code Flow. This allows the Developer to store the Webex access token as well as the refresh tokens to keep the access token up to date without any manual user intervention.

Regardless of which flow you end up deciding to implement, it all starts with a Webex Integration. Instead of walking you through that process here, we highly recommend following the [Getting Started Guide](https://developer.webex.com/docs/login-with-webex#getting-started). Once you have your Integration created, you can decide how you want your users to authenticate with Webex.

### Implicit Grant Flow Using the “id_token” Response Types

At a high level, the Implicit Grant Flow returns the Webex user’s information directly to the user’s address bar as part of the hash parameters that the Application Developer can then access. While this may sound complicated, it is transparent to the end user and quick to implement as a Developer.

Note that using this flow is one of the least secure methods, because by adding the identity in the web address, we open vulnerabilities due to network request logging and man-in-the-middle attacks. Read more about implicit grant flow [here](https://oauth.net/2/grant-types/implicit/)here.

The steps of the process are as follows:

1. Third-Party Application user clicks “Login with Webex”
2. Third-Party Application navigates to the [Webex Authorization endpoint](https://developer.webex.com/docs/login-with-webex#authorization-endpoint) with the response type of `id_token`
3. User allows Third-Party Application access to their Webex identity
4. Webex navigates back to the Third-Party Application with the ID Token added to the address (`example.com/myapp#id_token=abc123`)
5. Third-Party Application processes the ID Token by decoding it to get the Webex Identity
6. Third-Party Application uses the Webex Identity to authenticate

In order to experience these steps, we have a [code example](https://github.com/WebexSamples/login-with-webex) and [live demo](https://webexsamples.github.io/login-with-webex/openid3.html) of this flow available on GitHub.

#### Breaking Down the ID Token

The ID Token that is returned to the Third-Party Application is an encoded JSON Web Token (JWT) that contains information about the Webex user who just authorized the application. It will contain the user ID, email address, and more, depending on the OpenID scopes the requesting application has requested from Webex and the user has authorized Webex to send. Read more about ID Tokens in our documentation located [here](https://developer.webex.com/docs/login-with-webex#id-tokens).

### Authorization Code Flow with PKCE Using the “code” Response Types

A more secure method than the implicit flow is available for Developers. Unlike the Implicit Flow, the Authorization Code Flow brings in another component to the process: the back-end server. This flow is more secure because the token exchange happens on the Third-Party Application’s back-end server and not on the end user’s client. Instead of the ID Token being passed to the end user via a URI parameter, the Third-Party Application’s server will get access to the token instead and can then utilize it.

Login with Webex also steps up security by adding an additional layer of protection via the Proof Key for Code Exchange (PKCE, pronounced “Pixie”). If you’re familiar with basic Authorization Code flows, this is an additional step to validate that the information was requested by the originating server. The way PKCE works is the code challenge and verifier are generated on the requesting server, the challenge is sent with the authorization code request, and then when the access token exchange happens, the verifier is sent so that the Webex auth server knows the exchange came from the same source as the code request.

An overview of the steps of the process are as follows:

1. Third-Party Application user clicks “Login with Webex”
1. Third-Party Application generates a PKCE Code Challenge and Verifier
1. Third-Party Application navigates to the [Webex Authorization endpoint](https://developer.webex.com/docs/login-with-webex#authorization-endpoint) with the response type of “code” and the generated code challenge
1. User allows Third-Party Application access to their Webex identity
1. Webex navigates back to the Third-Party Application with the Authorization Code added to the address (`example.com/myapp?code=abc123`)
1. Third-Party Application processes the code and sends it to its back-end server
1. Third-Party Application’s back-end server exchanges the code for an access token and ID Token with the generated code verifier
1. Third-Party Application can use the access token to request more information about the Webex user via the [OpenID Connect Endpoints](https://developer.webex.com/docs/login-with-webex#oauth-20-and-openid-connect-api-endpoints).

In order to experience these steps, we have a [code example](https://github.com/WebexSamples/login-with-webex) and [live demo](https://webexsamples.github.io/login-with-webex/pkce.html) of this flow available on GitHub as well.

### Wrapping Up

We’re excited to add this capability to your application and look forward to seeing what you build with it! If you have feedback, suggestions, or you are encountering issues using Login with Webex, please reach out to our support team [https://developer.webex.com/support](https://developer.webex.com/support), and we will be happy to help! In addition, feel free to post questions (and answers) in our Webex Developer Community: [https://cs.co/WebexDeveloperCommunity](https://cs.co/WebexDeveloperCommunity).
