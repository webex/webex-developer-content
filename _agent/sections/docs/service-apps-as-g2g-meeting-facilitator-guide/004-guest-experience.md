---
type: Excerpt
canonical_url: https://developer.webex.com/docs/service-apps-as-g2g-meeting-facilitator-guide
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Guest Experience
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/service-apps-as-g2g-meeting-facilitator-guide). [Full Markdown](../../../../docs/service-apps-as-g2g-meeting-facilitator-guide.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

In this guide, we will explain how Service Apps in combination with a new subscription can be used to schedule meetings between only guests.



To request or manage this sandbox, open the [official portal page](<https://developer.webex.com/docs/service-apps-as-g2g-meeting-facilitator-guide>) and sign in.

[Need a Suite Sandbox?](<https://developer.webex.com/docs/developer-sandbox-guide>)

## Selected section

## Guest Experience

When guests click the join link, they can join the meeting either via an installed Webex native client or Webex browser. The guests can also be joined via our Webex SDKs to the meeting, usually from an Android or iOS device. If it is desired to have host control over a meeting, a join-link with host control can be generated, i.e. [startLink](https://developer.webex.com/meeting/docs/api/v1/meetings/join-a-meeting). This allows a guest to have full meeting controls, including the ability to manage the recording functions in the meeting, add additional guests dynamically, and more.

The following sections bring more color to the flow above. They work from the assumption that you had no previous exposure to Service Apps or guest-to-guest meetings.
