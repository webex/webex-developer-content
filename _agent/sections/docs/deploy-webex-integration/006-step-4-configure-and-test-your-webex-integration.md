---
type: Excerpt
canonical_url: https://developer.webex.com/docs/deploy-webex-integration
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- 'Step 4: Configure and test your Webex integration'
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/deploy-webex-integration). [Full Markdown](../../../../docs/deploy-webex-integration.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This tutorial describes deploying an example application on Heroku, and registering it as a Webex Integration.

---

# Deploy a Webex Integration

## Selected section

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
