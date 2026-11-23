---
type: Excerpt
canonical_url: https://developer.webex.com/docs/deploy-webex-integration
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- 'Step 2: Deploy on Heroku'
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/deploy-webex-integration). [Full Markdown](../../../../docs/deploy-webex-integration.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This tutorial describes deploying an example application on Heroku, and registering it as a Webex Integration.

---

# Deploy a Webex Integration

## Selected section

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
