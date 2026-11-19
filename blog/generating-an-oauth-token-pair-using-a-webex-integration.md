---
type: Article
title: Generating an OAuth Token pair using a Webex Integration
canonical_url: https://developer.webex.com/blog/generating-an-oauth-token-pair-using-a-webex-integration
content_type: blog
date: '2023-03-23'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/generating-an-oauth-token-pair-using-a-webex-integration)

In this blog post, we will help you to generate the OAuth Token pair (Access &amp; Refresh Token) using a Webex integration. Webex Integrations request permission to invoke Webex APIs on behalf of a User, whereas OAuth acts as an intermediary on behalf of the end user. It enables the applications to obtain limited access to a user’s data without sharing a user’s password. In case you would like to understand the OAuth process in more detail and how a Webex Integration is going to help there for generating the Token pair, for a complete walkthrough please review our blog post [Real world walkthrough of building an OAuth Webex integration](https://developer.webex.com/blog/real-world-walkthrough-of-building-an-oauth-webex-integration).

### Prerequisites

You need to create a Webex Integration first from our [Webex Developer Portal - Integrations](https://developer.webex.com/docs/integrations) documentation page and once the Integration is created successfully with all the required details, proceed further with the steps below.

### Possible Ways to Generate the Token Pair

We will discuss here two possible ways to generate the OAuth Token pair using Webex Integration and those are:

- Using POSTMAN
- Using our sample OAuth endpoint

&nbsp;

### Using POSTMAN

Postman is nothing but an API platform for building and testing APIs in the fastest possible ways. You can even automate certain tasks using APIs with Postman as well. That shows how powerful, but still lightweight application it is when we need to deal with APIs. You can visit [this](https://www.postman.com/) official website for Postman to download its Desktop App for your compatible OS.

Using POSTMAN should be straightforward and quick as we only need to fill out the Basic OAuth 2.0 Form with the required details to generate the Token pair.
Once you install the App, then go to POSTMAN and open a New HTTP Request Block. Once the fresh block opens up, visit the **Authorization** tab under the **Request** section and select the **Type** as *OAuth 2.0* from the dropdown list. It should provide a form where you need to enter the required details under **Configure New Token** section and the below screenshot from POSTMAN should guide you here.



> **Info**
>
> You can keep the entire **Enter request URL** section as blank since we’re going to provide the Request API URL in the OAuth 2.0 Form.



![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltf84a33e5983c6f80/64060cc299a3da109b6a7746/2.png)

After filling up the Configuration Form with the required details, please hit on the button *Clear cookies* so that it destroys the Postman Cache. Then, we need to click on **Get New Access Token** button and Postman would automatically redirect us to the browser to get ourselves authorized and generate the grant Code. In this step, please provide your Webex account credentials exactly using which you created the Webex integration and after the successful authorization, it would generate an Authentication complete pop-up as below:

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt8f05cbee4ec4443f/64060cc2c448032f744a8421/3.png)

And from here, either you can click on **Proceed** or, it would automatically redirect you to the **Token Details** page in just a few seconds as below:

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt9f38f0e3d4ba67f6/64060cc2952945362ea1aeb4/4.png)

From here, you can copy the generated Access and Refresh token pair in your personal notepad and start using them for your API Requests.
### Using our Sample OAuth Endpoint

Our sample OAuth endpoint was built specifically for the purpose of testing integration tokens without much of a hassle. It provides a GUI as represented on a screen capture below. It’s a semi-automated process where we will already capture the authentication code and redirect URI of the integration. You just need to feed the `clientId` and `clientSecret` of the Integration manually in the application to generate the Token pair.

Before further elaborating this option, please note that this URL, [https://oauth.webexbots.cloud/](https://oauth.webexbots.cloud/), should be kept as the only or, the first in the list (in case you want to keep more URLs) redirect URI in your Integration.

You might also keep the URLs in random order as per your choice, but in that case make sure you replace the value of `redirect_uri` as`https%3A%2F%2Foauth.webexbots.cloud%2F` (The URL encoded format of the above URL) in your integration OAuth authorization URL, after copying it to your preferred text file. This is necessary since [https://oauth.webexbots.cloud/](https://oauth.webexbots.cloud/) is the URL Endpoint where we have designed this OAuth mechanism which would help to generate the tokens and if this URL is not present in our Integration OAuth authorization URL, then we will never be redirected to this specific endpoint after a valid authorization. Hence, we need to follow any of the preferred ways as discussed here to keep this URL in the Integration OAuth Authorization URL.

Now let’s copy the entire OAuth authorization URL from the Integration and open it in a browser (use the Incognito/Private browser mode) followed by the authorization process where it asks for your Webex credentials authentication and once you’re authorized, our sample OAuth endpoint should open up with a basic Form where the `redirect_uri` and the authorization code will already be filled. We just need to insert the integration client ID and client secret and click **Request Access Token**. That should generate the token pair for us in the respective fields. The designed endpoint should look like the below image once the authorization code is generated:

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt1874ff165bd46ce4/64060cc2ff39cb107b871e49/5.png)

### Performing a sample API Request using this generated OAuth Integration Access Token

Since now we have the access and refresh token pair generated successfully, let’s try to perform a quick API Request using the access token. In this test, we will use the Postman tool to request the API. We have considered the Webex [Get My Own Details](https://developer.webex.com/docs/api/v1/people/get-my-own-details) REST API in this test which should provide our personal details in the response. Below is the screen capture to show where to insert the API URL for the request as well as how to use the generated access token:

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt02ac5b3ddb46bfb0/64060cc286d85210654b0730/6.png)



> **Info**
>
> The token **Type** should be selected as **Bearer Token** from the drop-down list while performing the API requests.



And with the successful `200 - OK` status code, the response should look like the following screen shot:

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltae7b2c924d54c905/64060cc252215a108d9221c2/7.png)

Please note, in this above example we have used a sandbox test user account just to show how an integration OAuth access token can be used for making Webex API requests and some of the confidential data in the response section have kept as hidden intentionally.

### FAQs

**Q**. *What should I select for the option **Will this Integration use a mobile SDK?** while creating the integration?*

**A**. If you’re creating the Integration for using the token in your Webex Mobile (iOS or, Android) SDKs authorization mechanism, please select the option *Yes*. Otherwise, if it’s just for performing regular API requests or, automating some of the functionalities using Webex APIs, please select the option *No*.

**Q**. *I don’t have a public redirect URL handy. Is it possible to create the Integration just for generating the token pair and performing some API Request tasks?*

**A**. Yes, you can still use a sample Redirect URI like, `https://localhost:8080/` or, `https://localhost:8080/login/` and that should be fine to create your token pair. If you’ve got a public redirect URI and you want to be directed to that specific page, after a successful authorization, please use that URI for this field.

**Q**. *What is the maximum number of redirect URIs I can use in a Webex Integration?*

**A**. There is no maximum limit currently for the Redirect URIs.

**Q**. *I’ve selected the meeting admin scopes `meeting:admin_XXX_XXX` in my Webex integration and there was no error while I was adding them. But in the generated token, I don’t see the scopes added. Why?*

**A**. Currently, the scopes with `meeting:admin_XXX_XXX` series in the Webex Integration Scope list are reserved only for Full Admin roles in an Org. If a regular user adds these scopes in their Webex integration, those will be marked as added and even it will not raise any error. However, these specific few scopes will not be reflected in the generated token. It is a known limitation which means being a normal user in an org - at this moment, there is no way to check the Org level meetings details.

**Q**. *How can I delete a Webex integration? If an integration is deleted, will my application(s) running on that integration’s token, be impacted?*

**A**. To delete a Webex Integration, please visit the page [https://developer.webex.com/my-apps](https://developer.webex.com/my-apps) and click on the integration name. Once the integration details are loaded, scroll down to the bottom of the page and click **Delete Integration**. That should delete your Integration.



> **Warning**
>
> Once the integration is deleted, all your applications where the token from this integration was used, will be definitely impacted.



**Q**. *Which one I should use when requesting an API, the Access token or the refresh token?*

**A**. For API Requests, use the Access token. A Refresh token is only used to generate a fresh access token once the corresponding access token expires.

**Q**. *What is the lifetime of Access tokens and Refresh tokens?*

**A**. By default, a Webex Access token’s lifetime is 14 days, and a Refresh token’s lifetime is 90 days. If the tokens are used in between their lifespan, again their lifetime gets defaulted.

**Q**. *How do I transfer the ownership of my integration to someone else in my organization?*

**A**. If you are a full admin in your organization, you can use our Ownership Transfer app [here](https://applications.webexbots.cloud/)

**Q**. *Is there any code sample showing how to design and build an authentication mechanism using a Webex Integration?*

**A**. Yes, there is one in Python language, using Flask framework. Details are here: [OAuth 2.0 with Webex in Flask](https://developer.webex.com/blog/using-oauth-2-with-webex-in-your-flask-application).

### Engage With Us

If you’ve got further questions or if you are still facing some technical issues while trying to generate the tokens, please reach out to us for support following the instructions provided on our [Webex Developer Support](https://developer.webex.com/support) page.

You can also join our [Webex Developer Community Forum](https://community.cisco.com/t5/webex-for-developers/welcome-to-the-webex-for-developers-forum/m-p/4558386#M321) which has dedicated topics, discussion groups, and announcements. We encourage you to tell us about your experience using the above provided example there.
