---
type: Excerpt
canonical_url: https://developer.webex.com/docs/service-apps
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Deauthorizing a Service App
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

## Deauthorizing a Service App

Any full admin in Control Hub can deauthorize a Service App. This often happens because an app is no longer needed or because of security concerns.

To deauthorize a Service App:

1. Go to **Management** &gt; **Apps** &gt; **Service Apps** and highlight the Service App. Uncheck the authorized checkbox and then click **Save**.
1. The machine account created during authorization is deleted, and the tokens are invalidated.

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltabb2c6cffe94faa7/642701bd068c4912c0fbb3ff/service-apps-guide-7.png)

If you created a `deauthorized` webhook for your Service Apps, Webex calls that webhook’s target URL when an admin deauthorizes the app.
