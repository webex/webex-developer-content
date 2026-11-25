---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-multistream-quick-start
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Kitchen Sink App
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-multistream-quick-start). [Full Markdown](../../../../../docs/sdks/webex-meetings-sdk-web-multistream-quick-start.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Setup Remote Media Event Listeners](004-setup-remote-media-event-listeners.md)

## Article introduction

With multistream, developers gain greater flexibility when displaying remote media streams. Instead of receiving a single stream featuring all participants, multistream enables the showcasing of multiple streams simultaneously. This means you can easily view each remote participant's stream individually, enhancing clarity and engagement during collaborative sessions.

---

This guide provides a quick glimpse into consuming multistream in Webex Meetings using the Webex JavaScript SDK. You'll find code snippets below that can quickly get you up and running.

## Selected section

## Kitchen Sink App

To experiment with more features of multistream, see the [Meeting Samples App](https://webex.github.io/webex-js-sdk/samples/browser-plugin-meetings/).

When using the sample app, in the **Manage Meeting** section, select the checkbox labeled **Use a multistream connection** (which automatically sets `enableMultistream` to true and passes it to the `join()` methods) before clicking on `Join Meeting` or `Join with Media`:

![Enable multistream in the sample app](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltc9074d83e5609144/enableMultistream.png)



> **Info**
>
> Enabling the **Use a multistream connection** replaces **Remote Video** fieldset with **Multistream Remote Videos** under the **Streams** section.
