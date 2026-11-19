---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-center-service-apps
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Introduction
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-center-service-apps). [Full Markdown](../../../../docs/contact-center-service-apps.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Decouple your most important business processes from individual user life cycles.

## Selected section

##  Introduction
Service apps enable you to request admin permission to use Webex Contact Center REST APIs, reducing dependence on a single user's authorization and mitigating any associated risks to your app. Instead, the actor for the API calls is a powerful machine account provisioned in the customer's org, ensuring your business automation flows will continue to run smoothly.

![create-new-app.png](https://s3.amazonaws.com/devportal.cms.intgus1/create_new_app_b39116809d.png)

Service Apps are often used for mission-critical business processes including:

-   End to end provisioning of users
-   Reporting dashboards for critical quality analysis
-   Onboard new Webex Contact Center users
-   … and much more.

Common to such apps is that they must run continually and be independent of any single user account. In contrast, for standard Integrations, if the authorizing user leaves the company or changes passwords, the Integration may break. In addition, unlike standard Integrations, Service Apps usually request data for many users and the whole org rather than on behalf of a single user.

Service Apps do share many similarities with Integrations. The industry standard  [OAuth 2.0 protocol](https://www.rfc-editor.org/rfc/rfc6749)  underpins both. OAuth client creation, scope selection, and authorization are happening just as they do for Integrations; however, those flows are mostly abstracted in a GUI experience for both the developer and the admins.

Two distinct personas are involved in putting a Service App into service: the developer and the full admin. Both of those workflows are described below.
