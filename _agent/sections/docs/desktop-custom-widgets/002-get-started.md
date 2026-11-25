---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-custom-widgets
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Get Started
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/desktop-custom-widgets). [Full Markdown](../../../../docs/desktop-custom-widgets.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Build and test Web Components and iframe widgets for Webex Contact Center Desktop.

## Selected section

## Get Started

We suggest to have a setup in which you are able to place your widget in a larger Desktop environment. For reference, you can use one of our boilerplate projects available at the Cisco DevNet Git Hub community: https://github.com/CiscoDevNet/webex-contact-center-widget-starter.

Alternatively, we suggest you to have a sandbox environment where you are able to place your widget (Web Component) in a constrained container and have an opportunity to test the following:

- Responsive behavior for various container sizes (from preferred to full screen).

  **Note:** Responsive web components make your webpage visually appealing on all devices and are easy to use. You must use responsive iFrame widgets. For more information, see [Create custom desktop layout](https://help.webex.com/en-us/article/ng08gqeb/Create-custom-desktop-layout) in Webex Help Center.

- Overflow behavior on how your widget appears and behaves when its contents overflow on either X or Y axis (that is, scrollbars).

- Reacting to data passed into the widget. For more information about reactive component practices, see [Reactive Property or Attribute Change](https://developer.webex.com/docs/desktop-custom-widgets#reactive-property-or-attribute-change).

- Light or Dark mode support (if you are using our Momentum UI Web Component library).
