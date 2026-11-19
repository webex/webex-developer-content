---
type: Guide
title: Register your App in the Developer Portal
display_title: Register Your App
canonical_url: https://developer.webex.com/docs/sdks/register-your-app
content_type: documentation
product_group:
- webex-suite
categories:
- calling
- meeting
- messaging
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/register-your-app)

To use the Webex Mobile SDK, you must register your app in the [Cisco Webex for Developers portal](https://developer.webex.com/).

---

This process generates a client ID and client secret for app authentication. You'll need to create a free Cisco Webex account if you don't have one.

1. Go to [Integration Registration](https://developer.webex.com/my-apps/new/integration).

2. Choose **Yes** for **Will this integration use a mobile SDK?**

    ![Image described in the surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltb57e765a8c01c86e/select_yes_for_sdk.png)

3. Name your integration. This appears on the user consent page.

    ![Image described in the surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt7c5551502cd6cba9/integration_name.png)

4. Enter a contact email for your app.

    ![Image described in the surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt39e9d4b5e8e9d476/developer_email.png)

5. Upload an app icon or choose a default one.

    ![Image described in the surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt9e31561d4392ae94/choose_icon.png)

6. Describe your app. This description appears on the consent page.

    ![Image described in the surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltab96aed04aa4b92a/app_description.png)

7. Enter redirect URIs for the **OAuth2** auth code capture. These URIs will be needed for the `OAuthAuthenticator`.

    ![Image described in the surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt80f3b2ba01c5d24e/redirect_uri.png)

8. Select **Add integration** to complete the registration.

    ![Image described in the surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltdafa1687eac74cc8/add_integration_button.png)

Congratulations, your integration is now created.
