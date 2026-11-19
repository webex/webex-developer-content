---
type: Excerpt
canonical_url: https://developer.webex.com/docs/deploy-webex-integration
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Objectives
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/deploy-webex-integration). [Full Markdown](../../../../docs/deploy-webex-integration.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This tutorial describes deploying an example application on Heroku, and registering it as a Webex Integration.

---

# Deploy a Webex Integration

## Selected section

## Objectives

As introduced in previous tutorials, Webex Integrations and Bots extend Webex’s capabilities.

By creating custom applications, developers can associate Webex with existing enterprise processes and data. For example, you may add the [Jira Integration](https://apphub.webex.com/applications/jira-cloud-34441) to an existing Room and get the participants notified when Jira issues (Epics, Story, Task, or Bugs), are created or updated.

Webex Integrations let your applications request permission to invoke the Webex API on behalf of other users. The process used to request permissions is called "OAuth Grant Flow": it is documented in the [Integrations guide](https://developer.webex.com/docs/integrations#requesting-permission), and can be experimented in the [Understand the OAuth Grant flow for Webex Integrations](https://developer-portal-intb.ciscospark.com/docs/understanding-oauth-flow-of-webex-integration) tutorial.

In this tutorial, we’ll go through an existing Node.js example that displays the name of Webex users. We will deploy it on Heroku, and register it as a Webex Integration.
