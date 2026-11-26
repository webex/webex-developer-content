---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-center-service-apps
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- 'Service App Creation: Admin Flow'
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-center-service-apps). [Full Markdown](../../../../docs/contact-center-service-apps.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Decouple your most important business processes from individual user life cycles.

## Selected section

## Service App Creation: Admin Flow


You have the following responsibilities as an admin who wants to use a Service App:

-   Be a Full Admin (read-only, device admins, etc., are insufficient).
-   Understand the purpose of the Service App, the developer's background, the scopes you are authorizing, and how your organization will use it.
-   Authorize the Service App for use in your org.

### Full Admin Authorization of a Service App

To authorize a service app:

1.  Log in to your organization's Control Hub ([https://admin.webex.com](https://admin.webex.com/)).
2.  Find the Service App you want to authorize. Service Apps can be found under  **Management**  >  **Apps**  >  **Service Apps**. If you cannot see the Service App in question, you need to ask the developer to have them submit for Admin Authorization or App Hub submission You can click the Service App and will see the service app’s description, developer info, and requested scopes.
3.  When ready to authorize the Service App, click  **Authorize**  followed by  **Save**. Your name is shown as the authorizing user in Control Hub. An entry in AdminAudit events is also created, documenting who authorized the Service App.
4.  Optionally, you may also wish to inform the developer that you have authorized their Service App.

![control-hub-service-app-list.png](https://s3.amazonaws.com/devportal.cms.intgus1/control_hub_service_app_list_7bdd663599.png)

### Deauthorizing a Service App

Any full admin in Control Hub can deauthorize a Service App. This often happens because an app is no longer needed or because of security concerns.

To deauthorize a Service App:

1.  Go to  **Management**  >  **Apps**  >  **Service Apps**  and highlight the Service App. Uncheck the authorized checkbox and then click  **Save**.
2.  The machine account created during authorization is deleted, and the tokens are invalidated.

![service-app-deauthorize.png](https://s3.amazonaws.com/devportal.cms.intgus1/service_app_deauthorize_2ae1ef5910.png)
