---
type: Excerpt
canonical_url: https://developer.webex.com/docs/deploy-webex-integration
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- 'Step 3: Register your Webex Integration'
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/deploy-webex-integration). [Full Markdown](../../../../docs/deploy-webex-integration.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This tutorial describes deploying an example application on Heroku, and registering it as a Webex Integration.

---

# Deploy a Webex Integration

## Selected section

## Step 3: Register your Webex Integration

The registration process is how your integration declares the set of authorizations required to execute its custom logic. It also specifies the redirect URL where our integration expects to receive the authorization code from Webex; from this authorization code, our integration will retrieve a time-limited access tokens, acting on behalf of the end-user.

1. Open the [“Create an Integration”](https://developer.webex.com/my-apps/new/integration) form on the "Webex for Developers" portal

1. Fill in the form with a name, a description, an email and an icon for your integration.

    The icon size must be 512x512 pixels or larger and publicly accessible, feel free to use this [DevNet logo png](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltb580504625714473/61eae0ecb05ddf268428b3e2/devNet-logo.png).

1. In the **Redirect URI(s)** field, paste the Heroku URL of your integration home page, replacing the index.html suffix with `/oauth`.

    In our example, the redirect URL is: `https://webex-integration.herokuapp.com/oauth`

    ![Fields](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt9f469f8ee3229580/61ead7537b3c5c6fe96c35e0/step3-fields.png)

1. The last field of the form concerns the OAuth scopes of your integration. These scopes correspond to the set of authorizations that the end-user will be asked to grant access for.

    For the sake of this tutorial, we will specify that our integration can ask for all supported authorizations, and we’ll refine these scopes at runtime.

    Check all scopes (except for `spark:all`) and click **Add integration**:

    ![Scopes](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt5f09a8303e7ac61f/61ead7539f6d8518d08ca23e/step3-scopes.png)

1. Webex automatically generates a **Client ID** and a **Client Secret** which we will use in the next step to configure our live integration running on Heroku.

    Keep this window opened or paste these values in a safe place:

    ![OAuth](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt98dfbb6c2b4d58d9/61ead753c0a40a27e868d959/step3-oauth3.png)
