---
type: Excerpt
canonical_url: https://developer.webex.com/docs/deploy-webex-integration
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- 'Step 1: Fork a Webex integration'
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/deploy-webex-integration). [Full Markdown](../../../../docs/deploy-webex-integration.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This tutorial describes deploying an example application on Heroku, and registering it as a Webex Integration.

---

# Deploy a Webex Integration

## Selected section

## Step 1: Fork a Webex integration

For the sake of this tutorial, we will leverage a [ready-to-run Webex Integration](https://github.com/CiscoDevNet/webex-integration-sample).

This integration example consists of a Node.js server that serves as a HTML page to initiate the Webex OAuth 'authorization code grant' flow. This page drives the user to a consent form. The integration also listens on a “redirect URL” invoked by Webex, as the end-user accepts or declines to manage permissions.

![OAuth](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt622caaca9768812d/61ead7538cd123267e7d2346/step1-oauth.png)

Open the [Webex Integration example](https://developer-portal-intb.ciscospark.com/docs/understanding-oauth-flow-of-webex-integration#step-1-sign-up-for-webex-and-take-a-tour) provided for this tutorial. Make sure you're signed in on Github.

Click "Fork" to start working on your own copy of this integration.
