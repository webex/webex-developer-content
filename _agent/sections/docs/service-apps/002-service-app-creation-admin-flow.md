---
type: Excerpt
canonical_url: https://developer.webex.com/docs/service-apps
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- 'Service App Creation: Admin Flow'
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/service-apps). [Full Markdown](../../../../docs/service-apps.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Decouple your most important business processes from individual user life cycles.

---

Service apps enable you to request admin permission to use Webex REST APIs, reducing dependence on a single user's authorization and mitigating any associated risks to your app. Instead, the actor for the API calls is a powerful machine account provisioned in the customer's org, ensuring your business automation flows will continue to run smoothly.

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt8766b07df737c0c4/642701bd2e3e5f1225cc19f2/service-apps-guide-1.png)

Service Apps are often used for mission-critical business processes including:

- End to end provisioning of users
- Reporting dashboards for critical quality analysis
- Meeting scheduling systems
- Onboard new Webex calling users
- As part of BYODS [Bring your own Datasource](https://developer.webex.com/docs/bring-your-own-datasource)
- … and much more.

Common to such apps is that they must run continually and be independent of any single user account. In contrast, for standard Integrations, if the authorizing user leaves the company or changes passwords, the Integration may break. In addition, unlike standard Integrations, Service Apps usually request data for many users and the whole org rather than on behalf of a single user.

Service Apps do share many similarities with Integrations. The industry standard [OAuth 2.0 protocol](https://www.rfc-editor.org/rfc/rfc6749) underpins both. OAuth client creation, scope selection, and authorization are happening just as they do for Integrations; however, those flows are mostly abstracted in a GUI experience for both the developer and the admins.

Two distinct personas are involved in putting a Service App into service: the developer and the full admin. Both of those workflows are described below.

## Selected section

## Service App Creation: Admin Flow

You have the following responsibilities as an admin who wants to use a Service App:

- Be a Full Admin (read-only, device admins, etc., are insufficient).
- Understand the purpose of the Service App, the developer's background, the scopes you are authorizing, and how your organization will use it.
- Authorize the Service App for use in your org.

### Full Admin Authorization of a Service App

To authorize a service app:

1. Log in to your organization's Control Hub ([https://admin.webex.com](https://admin.webex.com)).
1. Find the Service App you want to authorize under **Management** &gt; **Apps** &gt; **Service Apps**. If it is missing, ask the developer to request admin authorization for an app in your organization or complete App Hub submission and review for an external app. Click the Service App to review its description, developer information, and requested scopes.
1. When ready to authorize the Service App, click **Authorize** followed by **Save**. Your name is shown as the authorizing user in Control Hub. An entry in AdminAudit events is also created, documenting who authorized the Service App.
1. Optionally, you may also wish to inform the developer that you have authorized their Service App.

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt4b933c95aae36841/642701bd79ce221199ffaeb2/service-apps-guide-6.png)
