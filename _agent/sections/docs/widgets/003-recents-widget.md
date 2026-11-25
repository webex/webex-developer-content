---
type: Excerpt
canonical_url: https://developer.webex.com/docs/widgets
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Recents Widget
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/widgets). [Full Markdown](../../../../docs/widgets.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Embed the power of Webex in your web applications ✨

## Selected section

## Recents Widget

Include a user's most recent Webex spaces in your app and respond to real-time events.
This widget displays a list of recent Webex spaces and can act as a central event processing hub for events happening within the Webex Platform.

[GitHub](<https://github.com/webex/react-widgets/tree/master/packages/node_modules/@webex/widget-recents#webex-recents-widget-webexwidget-recents>)
[Demo App](<https://code.s4d.io/widget-demo/production/index.html>)

### Recents Widget Features



  <ul>
    <li>Recent Webex conversation list (spaces & people)</li>
    <li>Hooks to open a conversation with the Space Widget</li>
    <li>Unread space highlighting</li>
    <li>Event hooks for messages, meetings, and memberships</li>
    <li>Incoming call notifications</li>
    <li>FedRAMP environment support. See the <a href="https://github.com/webex/widgets#fedramp-environment">usage README</a>.</li>
  </ul>


  <img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltf7f2462ef3ae82f5/61b38353a342a6586354334d/Recents.png" title="Recents widget" width="100%" />



### Recents Widget Usage

To use this widget, you'll first need to create an [integration](https://developer.webex.com/docs/integrations) with the following scopes: `spark:all`.

Using our CDN requires the least amount of work to get started. Add the following to your HTML file:

```html
<!-- Production compiled and minified CSS -->
<link rel="stylesheet" href="https://code.s4d.io/widget-recents/production/main.css">

<!-- Production compiled and minified JavaScript -->
<script src="https://code.s4d.io/widget-recents/production/bundle.js"></script>
```

You can then instantiate the widget by providing an `ACCESS_TOKEN`:

```html
<div id="my-recents-widget" />

<script>
  // Grab DOM element where widget will be attached
  var widgetEl = document.getElementById('my-recents-widget');

  // Initialize a new Recents widget
  webex.widget(widgetEl).recentsWidget({
    accessToken: 'ACCESS_TOKEN'
  });
</script>
```

If you'd like to use a guest token instead of an access token, use the `guestToken` parameter with a guest token instead of `accessToken`.

For more usage and configuration information, see the [Recents Widget Usage](https://github.com/webex/react-widgets/tree/master/packages/node_modules/@webex/widget-recents#usage) documentation in GitHub.

### Recents Widget Events

The Recents Widget exposes a few events for hooking into widget functionality.
When instantiating a Recents widget, you can provide a callback parameter that will fire whenever an event occurs.
You can then filter the actions and perform actions:

```html
<div id="my-recents-widget" />

<script>
  // Grab DOM element where widget will be attached
  var widgetEl = document.getElementById('my-recents-widget');

  // Initialize a new Recents widget
  webex.widget(widgetEl).recentsWidget({
    accessToken: 'ACCESS_TOKEN',
    onEvent: callback
  });

  function callback(name, detail) {
    if (name === 'messages:created') {
      // Perform an action if a new message has been created
    }
  }
</script>
```

See the [Recents Widget Events](https://github.com/webex/react-widgets/tree/master/packages/node_modules/@webex/widget-recents#events) documentation in GitHub for more information about event handling.

### Recents Widget Requirements

Supported Desktop Browsers: Chrome (latest), Firefox (latest), and Safari (latest)

Please note the Recents Widget _is not supported on Mobile browsers_.
