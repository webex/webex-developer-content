---
type: Excerpt
canonical_url: https://developer.webex.com/docs/service-apps-as-g2g-meeting-facilitator-guide
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Service Apps as Guest-to-Guest Meeting Facilitators
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/service-apps-as-g2g-meeting-facilitator-guide). [Full Markdown](../../../../docs/service-apps-as-g2g-meeting-facilitator-guide.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

In this guide, we will explain how Service Apps in combination with a new subscription can be used to schedule meetings between only guests.



To request or manage this sandbox, open the [official portal page](<https://developer.webex.com/docs/service-apps-as-g2g-meeting-facilitator-guide>) and sign in.

[Need a Suite Sandbox?](<https://developer.webex.com/docs/developer-sandbox-guide>)

## Selected section

## Service Apps as Guest-to-Guest Meeting Facilitators

In the guest-to-guest meeting scenario, we are using the Service App as the meeting orchestrator for guest-to-guest meetings. If you think back about what makes Service Apps special, our design decision may be immediately apparent. The app needs to run on an ongoing basis, and we cannot risk the app stop working because a user leaves or changes their password. The app also needs access to meeting functionality to schedule, monitor and report on meetings. The alternative application type would have been a user-authorized `integration` with the danger that the user either leaves or is accidentally being deleted or changes their password, all of which would render the tokens invalid.

### Service Apps as Guest Creator

Guests are temporary, unnamed, and unlicensed users. Guests are used where a named user license doesn’t make sense or where an interaction in Webex is tightly time-bound. For example, when a customer launches the Webex meetings or chat widget from a company website, this customer most likely doesn’t need to interact through Webex on an ongoing basis. Instead, they should be supplied with a temporary identity that allows them to interact with the agent, which will be discarded after the exchange.

Guests in the past were created through a different app type called the Guest Issuer. However, we are changing the guest creation and now let Service Apps create guests. The biggest advantage to guest creation via Service Apps is that the flow is now inherently admin-approved. Guest creation via guest issuer is possible by any developer in an organization, without admin approval. With the old Guest Issuer flow, the guest organizations are not admin-managed, and admins had no insight into which guests were created in the org. With the new approach, guests can only be created after an admin approves the Service App in the Control Hub. Admins can also query the number of guests created by the Service App.



> **Warning**
>
> Guest Issuer guests are considered deprecated and will be removed in the future



### Guest-To-Guest Subscriptions, Guest Sites, and Licenses

We offer a new subscription for `guest-to-guest` meetings and, with it, a new license. Remember, guest-to-guest meetings or, more broadly, meetings without the sponsor of a license were and are a terms and conditions violation. Now, the Service App takes on the role of the license sponsor. The Service App does not need to participate in the meeting. It does need to schedule the meeting and may create the guests that ultimately join the meeting. In contrast to a regular user, the Service App can sponsor as many simultaneous meetings as are allowed by the subscription. When procuring the subscription, the partner orders a certain number of concurrent meetings.

For example, Let’s say the partner ordered `150` meetings with the subscription. This means the Service App can sponsor up to `150` meetings in the `inProgress` state at the same time; in other words, it can host up to `150` simultaneous meetings. When there are `150` meetings ongoing and a guest tries to start the 151st meeting, by clicking the join link or joining via the SDK, a license error is issued. Each meeting can have up to 400 participants joining.

Service Apps in the guest-to-guest flow are bonded during the authorization process to a specially configured and marked site, the guest-to-guest site. The site is set up in the organization when an admin activates the subscription via the provisioning wizard. The admin determines and assigns the site name, which, like any other site setup, must be globally unique. The necessary configuration for this guest-to-guest site is done by our backend system. Only the Service App is allowed as a user on this site. Guests join guest-to-guest meetings, but are not part of the guest-to-guest site.

### Webhook Notification

The Service App developer’s organization and the organization where the guest-to-guest meetings happen are not necessarily the same. In fact, for most applications, the developer and the authorizing admin are in separate organizations. The developers need to be informed of the authorization of the Service App by the admin, for them to retrieve the tokens. To that end, we provide a webbook with the resource `serviceApp` and the event type `authorized` and `deauthorized`. When the admin authorizes the Service App a webhook is sent to the registered `targetURL`. The webhook contains information about the Service App like the scopes granted and also the list of guest-to-guest sites the Service App was authorized for. With the webhook, the developer knows they can retrieve the tokens to call the APIs. They also know for which Webex sites these tokens can be used to schedule meetings. When an admin deauthorizes a Service App the tokens get invalidated. The developer will receive a `serviceApp:deauthorized` webhook.
