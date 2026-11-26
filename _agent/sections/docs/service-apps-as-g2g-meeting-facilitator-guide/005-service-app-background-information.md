---
type: Excerpt
canonical_url: https://developer.webex.com/docs/service-apps-as-g2g-meeting-facilitator-guide
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Service App Background Information
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/service-apps-as-g2g-meeting-facilitator-guide). [Full Markdown](../../../../docs/service-apps-as-g2g-meeting-facilitator-guide.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

In this guide, we will explain how Service Apps in combination with a new subscription can be used to schedule meetings between only guests.



To request or manage this sandbox, open the [official portal page](<https://developer.webex.com/docs/service-apps-as-g2g-meeting-facilitator-guide>) and sign in.

[Need a Suite Sandbox?](<https://developer.webex.com/docs/developer-sandbox-guide>)

## Selected section

## Service App Background Information

### What are Service Apps

Service Apps represent an application type in the Webex developer program. They are recommended for apps that are mission-critical, long-lived and they are often needed for some kind of admin functionality. We see them most often used for ongoing provisioning or reporting systems. Service Apps are at the intersection of two other application types: `bots` and `integrations`.

They borrow from bots their independent nature. A machine account is created in the authorizer’s organization when a Service App is authorized. The developer retrieves the token for each organization’s machine account as an individual access and refresh token pair. All API calls made with the Service App tokens are made on behalf of this machine account. Since the machine account is not managed directly, it cannot be accidentally deleted, or manipulated in other ways that would make the app stop working. From `integrations`, they borrow the concept of scopes as well as the need to be authorized; both are implemented as oAuth clients.

Scopes determine the API calls that the Service App is allowed to make. Service App authorization happens in the Control Hub GUI and must be done by a Full Admin. You can think of Service Apps as bots with scopes. Bot tokens also have a long lifetime and represent machine accounts.

### Choosing a Bot or a Service App

When confronted with the decision between a `bot` or a Service App as your application type, you should decide with the *least privilege principle*. If a `bot` can get you all the functions you need, you should use the `bot` application type. However, `bots` have the following limitations:

- They cannot be compliance officers.
- They cannot be admins.
- They cannot see messages that are not addressed to them. 
- They are unaware of meetings or media (audio/video) (the reason why we cannot use them for our guest-to-guest meetings).

If you need any kind of admin functionality or any of the capabilities just mentioned you need to use a Service App like we do for our guest-to-guest flow. For now, Service Apps always have an admin role.
