---
type: Excerpt
canonical_url: https://developer.webex.com/docs/widgets
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Space Widget
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/widgets). [Full Markdown](../../../../docs/widgets.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Embed the power of Webex in your web applications ✨

## Selected section

## Space Widget

Include Webex space functionality in your app.
This widget provides messaging, meeting and content sharing features related to spaces.
Join 1:1 or group spaces to collaborate via messaging or start and join meetings, all with the familiar Webex UI.

[GitHub](<https://github.com/webex/react-widgets/tree/master/packages/node_modules/@webex/widget-space#webex-space-widget-webexwidget-space>)
[Demo App](<https://code.s4d.io/widget-demo/production/index.html>)

### Space Widget Features



  <ul>
    <li>
      Messaging:
      <ul>
        <li>1:1 and group messaging</li>
        <li>Markdown message support</li>
        <li>File sharing. (150MB file size limit)</li>
        <li>Delete/flag messages</li>
        <li>Read receipts</li>
        <li>Persistent chat</li>
        <li>Roster list and @mention</li>
      </ul>
    </li>
    <li>
      Meetings:
      <ul>
        <li>Join 1:1/Group Space meetings using password or hostkey based authentication</li>
        <li>Dial by email address or SIP address.
          <i><b>Note:</b> SIP addresses are only supported for Webex meetings SIP URIs and not for Webex Calling or 3rd party SIP URIs</i></li>
        <li>Share screen or a specific application/browser tab. Note: Safari browsers ONLY support sharing the whole screen</li>
      </ul>
    </li>
    <li>FedRAMP environment support. See the <a href="https://github.com/webex/widgets#fedramp-environment">usage README</a>.</li>
  </ul>


  <img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt8d57b2446b4648ca/61b383539a45fb1280c1938d/Space-Widget-Messaging.png" title='Messaging on Space Widget' width="100%" />



### Space Widget Usage

To use this widget, you'll first need to create an [integration](https://developer.webex.com/docs/integrations) with the following scopes: `spark:all`.

Using our CDN requires the least amount of work to get started. Add the following to your HTML file:

```html
<!-- Latest compiled and minified CSS -->
<link rel="stylesheet" href="https://code.s4d.io/widget-space/production/main.css">

<!-- Latest compiled and minified JavaScript -->
<script src="https://code.s4d.io/widget-space/production/bundle.js"></script>
```

You can then instantiate the widget by providing an `ACCESS_TOKEN` and `SPACE_ID`:

```html
<div id="my-space-widget" />

<script>
  // Grab DOM element where widget will be attached
  var widgetEl = document.getElementById('my-space-widget');

  // Initialize a new Space widget
  webex.widget(widgetEl).spaceWidget({
    accessToken: 'ACCESS_TOKEN',
    destinationType: 'spaceId',
    destinationId: 'SPACE_ID'
  });
</script>
```

If you'd like to use a guest token instead of an access token, use the `guestToken` parameter with a guest token instead of `accessToken`.

For more usage and configuration information, see the [Space Widget Usage](https://github.com/webex/react-widgets/blob/master/packages/node_modules/%40webex/widget-space/README.md#usage) documentation in GitHub.

### Space Widget Requirements

Supported Desktop Browsers: Chrome (latest), Firefox (latest), and Safari (latest).

Please note that Space Widget _is not supported on Mobile browsers_.
