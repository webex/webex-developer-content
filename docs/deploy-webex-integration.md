---
type: Guide
title: Deploy a Webex Integration
display_title: Deploy a Webex Integration
canonical_url: https://developer.webex.com/docs/deploy-webex-integration
content_type: documentation
product_group:
- webex-suite
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/deploy-webex-integration)

This tutorial describes deploying an example application on Heroku, and registering it as a Webex Integration.

---

# Deploy a Webex Integration

## Objectives

As introduced in previous tutorials, Webex Integrations and Bots extend Webex’s capabilities.

By creating custom applications, developers can associate Webex with existing enterprise processes and data. For example, you may add the [Jira Integration](https://apphub.webex.com/applications/jira-cloud-34441) to an existing Room and get the participants notified when Jira issues (Epics, Story, Task, or Bugs), are created or updated.

Webex Integrations let your applications request permission to invoke the Webex API on behalf of other users. The process used to request permissions is called "OAuth Grant Flow": it is documented in the [Integrations guide](https://developer.webex.com/docs/integrations#requesting-permission), and can be experimented in the [Understand the OAuth Grant flow for Webex Integrations](https://developer-portal-intb.ciscospark.com/docs/understanding-oauth-flow-of-webex-integration) tutorial.

In this tutorial, we’ll go through an existing Node.js example that displays the name of Webex users. We will deploy it on Heroku, and register it as a Webex Integration.

## Pre-requisites

In this learning tutorial, you will deploy an example application on Heroku, and register it as a Webex Integration.

You will need:

- a Webex Developer account: if you're not yet a Webex User, you can [sign up here](https://www.webex.com/products/teams/index.html),
- a GitHub account: [sign up here](https://github.com/join) if you are not already a GitHub user,
- a Heroku Account: [click here](https://signup.heroku.com) to signup at Heroku.

**Note**: For this tutorial, we’ll stick to [Heroku free dynos](https://devcenter.heroku.com/articles/free-dyno-hours), so that the deployment won’t cost you any money.

## Step 1: Fork a Webex integration

For the sake of this tutorial, we will leverage a [ready-to-run Webex Integration](https://github.com/CiscoDevNet/webex-integration-sample).

This integration example consists of a Node.js server that serves as a HTML page to initiate the Webex OAuth 'authorization code grant' flow. This page drives the user to a consent form. The integration also listens on a “redirect URL” invoked by Webex, as the end-user accepts or declines to manage permissions.

![OAuth](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt622caaca9768812d/61ead7538cd123267e7d2346/step1-oauth.png)

Open the [Webex Integration example](https://developer-portal-intb.ciscospark.com/docs/understanding-oauth-flow-of-webex-integration#step-1-sign-up-for-webex-and-take-a-tour) provided for this tutorial. Make sure you're signed in on Github.

Click "Fork" to start working on your own copy of this integration.

## Step 2: Deploy on Heroku

The goal of this step is to create the Heroku project that will host our integration and retrieve its public URL.

Heroku is a cloud application platform that lets you deploy and run code in minutes.

Note that the example provided in this tutorial can be hosted on other private or public cloud application platforms, such as Amazon Web Services, Microsoft Azure, Google Cloud, Clever Cloud Enterprise...

If you don’t have a Heroku account yet, you can signup at <https://signup.heroku.com/>. Note that for development and prototyping purpose, we’ll stick to Heroku [free dynos](https://devcenter.heroku.com/articles/free-dyno-hours) so that the deployment covered won’t cost any money.

1. Log on to your [Heroku dashoard](https://dashboard.heroku.com/new?org=personal-apps) and create a brand new application:

    ![](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt290d03e0858be3d4/61ead753ecbd3f1a43faabc8/step2-heroku-new-app.png)

1. Once created, Heroku displays your application deployment configuration. The default deployment method is to use Heroku Git.

    For the purpose of this tutorial, we will deploy straight from GitHub, skipping the installation of the Heroku command line interface.

    Click the **GitHub** option. Among your GitHub repositories, select the webex-integration-sample” project you forked in step 1, and click **Connect**:

    ![Connect](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt50120db36a7828ac/61ead75305090f6fde9c866f/step2-connect.png)

    You will end up with a Heroku deployment configuration similar to the one below:

    ![Connected](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt7d7d5a41f76755ce/61ead753f7892a49a7b0b230/step2-connected.png)

1. Now, click the **Deploy Branch** button, and watch Heroku build and deploy your code sample:

    ![Manual](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltf8d8c68feaad95ba/61ead75396465f4b1220f726/step2-manual.png)

1. When done, click **View** to open your app's entry point. An HTML page such as the one below should appear:

    ![Template](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt9a970fc7e3843d97/61ead753b05ddf268428b3be/step2-ejs.png)

    >Don't run the OAuth flow for now, as we first need to register the integration to Webex

1. Keep the root URL of your integration in a safe place as we’ll need it in the next step.

    The root URL in the example above is: <https://webex-integration.herokuapp.com/>

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

## Step 4: Configure and test your Webex integration

In this last step, we'll configure your Webex integration running on Heroku.

1. Go to the settings tab of your Heroku project and click **Reveal Config Vars**

1. Add new variables for the `CLIENT_ID`, `CLIENT_SECRET` and `REDIRECT_URI` declared previously, and enter in their respective values

    ![Personal Apps](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt760b4db5715e3285/61ead7537ac77518d6ec20d2/step4-personalapps.png)

1. As you add or modify any "Config" variable, Heroku automatically restarts your integration so that you’ll be happy to notice that your integration is now running live and ready to be invoked.

    In the upper-right click **Open App**, and experiment with your Webex Integration live:

    ![Example](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltb3a15287d7fcdb5a/61ead76405090f6fde9c8673/testing.png)

### Going further

What about making your integration list the rooms the Webex end-user has access to?

Tips: Edit the GitHub project you forked in step 1 and:

- Change the OAuth permission with the `spark:rooms_read` scope

- Switch the EJS template to the `rooms-list.ejs` template provided

- Load the user’s list of rooms by calling the [Webex API List Rooms](https://developer.webex.com/docs/api/v1/rooms/list-rooms) resource
