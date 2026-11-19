---
type: Article
title: Login with Webex on Developer Applications and 3rd Party Platforms
canonical_url: https://developer.webex.com/blog/login-with-webex-on-developer-applications-and-3rd-party-platforms
content_type: blog
date: '2022-09-06'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/login-with-webex-on-developer-applications-and-3rd-party-platforms)

Webex enters a brave new world of allowing users and developers the ability to use their Webex Identity to authenticate to our partners platforms or on a device that does not have a keyboard. Login with Webex removes friction for users and makes their experience 10x better. Webex demonstrated this login capability at Cisco Live where a user can move their meeting from a laptop to a mobile device and for Ford or Facebook when the user logs in a device without a keyboard.

This cross functional team worked diligently for six months across the entire platform to prove the model and test with partners like Ford and Facebook. They built this feature using the [OpenID Connect Standard](https://openid.net/connect/) so that Security was built in not bolted on. [Embebedded Applications](https://developer.webex.com/docs/embedded-apps) were a key business reason for the new capability, to remove friction when users did no have an account on the partner's platform, so the client team engaged with partners to prove the model would work. The feature has been deployed on [developer.webex.com](https://developer.webex.com) for all our developer teams to use with world class documentation and developer support.

### Key Features supported

Login with Webex supports the following OAuth flows:

- [Authorization Code Flow](https://developer.webex.com/docs/login-with-webex#authorization-code-flow) and [Authorization Code Flow with PKCE](https://developer.webex.com/docs/login-with-webex#authorization-code-flow-with-proof-key-for-code-exchange) for devices with a web browser and keyboard. Authorization Code Flow with PKCE is the recommended flow as it provides the best security.
- [Device Grant Flow](https://developer.webex.com/docs/login-with-webex#device-grant-flow) is designed for smart TVs and other devices without a web browser or with limited input abilities. Note that Device Grant flow does not support [OpenID Connect scopes](https://developer.webex.com/docs/login-with-webex#openid-connect-scopes-and-claims).
- [Implicit Grant Flow](https://developer.webex.com/docs/login-with-webex#implicit-grant-flow) allows an OAuth client to obtain access and ID tokens directly from the authorization server in a single request. This flow is discouraged from use due to security concerns.

&nbsp;

### OAuth 2.0 and OpenID Connect API Endpoints

OpenID Connect is built on the OAuth 2.0 protocol, the same protocol used by Webex [Integrations](https://developer.webex.com/docs/integrations) to get permission from a user to make Webex API calls on their behalf. With Webex OAuth 2.0 APIs you can both obtain an ID token that proves the user has authenticated with Webex, and an access token to make API calls.

- [Authorization Endpoint](https://developer.webex.com/docs/login-with-webex#authorization-endpoint)
- [Device Authorization Endpoint](https://developer.webex.com/docs/login-with-webex#device-authorization-endpoint)
- [Access Token Endpoint](https://developer.webex.com/docs/login-with-webex#access-token-endpoint)
- [Device Token Endpoint](https://developer.webex.com/docs/login-with-webex#access-token-endpoint)
- [UserInfo Endpoint](https://developer.webex.com/docs/login-with-webex#userinfo-endpoint)
- [Verification Endpoint](https://developer.webex.com/docs/login-with-webex#verification-endpoint)
- [Discovery Endpoint](https://developer.webex.com/docs/login-with-webex#discovery-endpoint)
- [Webfinger Endpoint](https://developer.webex.com/docs/login-with-webex#webfinger-endpoint)

&nbsp;

### Product Documentation

The home for Login with Webex documentation is on the Webex Developer Portal at [https://developer.webex.com/docs/login-with-webex](https://developer.webex.com/docs/login-with-webex)

### Demo of the Ford Lightning

&nbsp;

<iframe width="560" height="315" src="https://www.youtube.com/embed/kd_HwyTX1lg" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
[https://www.youtube.com/watch?v=kd_HwyTX1lg](https://www.youtube.com/watch?v=kd_HwyTX1lg)

&nbsp;

### Apple Move Meeting from Mac to Mobile

&nbsp;

<iframe width="560" height="315" src="https://www.youtube.com/embed/Aj100uP9QGc" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
[https://youtu.be/Aj100uP9QGc](https://youtu.be/Aj100uP9QGc)

&nbsp;

### Your Feedback Matters

If you have feedback, suggestions, or you are encountering issues using the Login with Webex tools, please reach out to our support team [https://developer.webex.com/support](https://developer.webex.com/support), and we will be happy to help! In addition, feel free to post questions (and answers) in our [Webex Developer Community](https://cs.co/WebexDeveloperCommunity).
