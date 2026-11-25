---
type: Excerpt
canonical_url: https://developer.webex.com/docs/using-the-webex-space-widget-for-video-and-messaging
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Add the Widget to an HTML page
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/using-the-webex-space-widget-for-video-and-messaging). [Full Markdown](../../../../docs/using-the-webex-space-widget-for-video-and-messaging.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Selected section

## Add the Widget to an HTML page

In the previous steps, you experienced the messaging and video capabilities of the Space widget in a 1-on-1 Space.  We'll now show you how developers can add the Widgets into existing web sites and applications.

The Space Widget Demo page you just used to test your Widget also displays a sample code snippet pre-populated with your configured options, ready to copy-and-paste into a web page.  

Let's give it a try:

1. On the Widget demo page, scroll down to the **Space Widget Example Code** section.

1. Examine the sample snippet, which includes an HTML `<div>` element that will act as the Widget container, along with some JavaScript code that instantiates the widget on page load:

    ![Example generated code snippet](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt9d19e986ef7d8496/61e8807e78c11410d82de322/code-snippets.png)

1. Using your favorite text editor create a new file named `widget.html`, and copy/paste in the example code into the page body.

1. Replace the `'XXXXXXXXXXXXXXXX'` place holder with your personal access token retrieved previously, and save your changes.

1. Open the `widget.html` file in a Web browser, and start collaborating!



> **Warning**
>
> Note that in a real-world applications you should **not** hard-code access tokens into your web application in this way. For production apps, [Webex Integrations](https://developer.webex.com/docs/integrations) provides the mechanism to securely authenticate users and obtain access tokens dynamically and safely.
