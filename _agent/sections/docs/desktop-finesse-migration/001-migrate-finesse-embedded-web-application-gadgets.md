---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-finesse-migration
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Migrate Finesse Embedded Web Application Gadgets
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/desktop-finesse-migration). [Full Markdown](../../../../docs/desktop-finesse-migration.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Migrate embedded Finesse applications and refactor JavaScript gadgets into Desktop widgets.

## Selected section

## Migrate Finesse Embedded Web Application Gadgets

You can migrate a Finesse embedded web application gadget into a Webex Contact Center Desktop iFrame based widget.

**Note:** Conversion of a Finesse gadget depends on the web application configuration-whether it could be loaded in an iFrame or not.

### Finesse—Embedded Web Application Sample Gadget

The embedded web application sample gadget displays a web page in an iFrame within the gadget. It is intended to serve as an example of placing an external web application in the Finesse gadget.

For more information on the embedded web application sample gadget, see https://github.com/CiscoDevNet/finesse-sample-code/tree/master/EmbeddedWebAppSampleGadget.

### Webex Contact Center Desktop—agentx-wc-iframe

Desktop has the inbuilt functionality (Web Component) to load web applications in an iFrame. Using the component `agentx-wc-iframe` within the desktop layout, you can load web applications in the horizontal header, navigation bar, and auxiliary information pane.

For more information on Webex Contact Center Desktop widgets, see https://github.com/CiscoDevNet/webex-contact-center-widget-starter/tree/master/Examples.

The following are the Finesse embedded gadget files:

- EmbeddedWebApp.css
- EmbeddedWebApp.js
- EmbeddedWebApp.xml

The EmbeddedWebApp.xml is the main file that contains the URL of the web application. Replace `https://widget.example.com/embedded-app` in every example with your controlled application URL. Its response must permit framing by your approved Desktop origins, as described in [iframe widget CSP configuration](https://developer.webex.com/docs/desktop-custom-widgets#iframe-widgets).

**Before you begin**

Understand the `script type` details from the Finesse embedded gadget file EmbeddedWebApp.xml.

```html
<script type="text/javascript">
    // initialize the gadget running the init handler defined in EmbeddedWebApp.js
    gadgets.HubSettings.onConnect = function () {
        finesse.modules.EmbeddedWebAppGadget.init("https://widget.example.com/embedded-app");
    };
</script>
```

Understand the JSON layout format. For more information on JSON layout, see [Create custom desktop layout](https://help.webex.com/en-us/article/ng08gqeb/Create-custom-desktop-layout) in Webex Help Center.

**Procedure**

Step 1: Access the JSON layout file from the Webex Contact Center Management Portal.

Step 2: In the `comp` property tag, enter the component value as `agentx-wc-iframe`.

```json
{
    "comp": "agentx-wc-iframe"
}
```

Step 3: In the `src attributes` property tag, enter the URL of the web application.

```json
{
    "comp": "agentx-wc-iframe",
    "attributes": {
        "src": "https://widget.example.com/embedded-app"
    }
}
```

Step 4: In the `wrapper` property tag, enter the title and the maximize area name.

```json
{
    "comp": "agentx-wc-iframe",
    "attributes": {
        "src": "https://widget.example.com/embedded-app"
    },
    "wrapper": {
        "title": "AgentX iFrame",
        "maximizeAreaName": "app-maximize-area"
    }
}
```

Step 5: Use the `style` property tag to resize the iFrame.

**Note:** The iFrame within the Desktop supports native iFrame properties.

```json
{
    "comp": "agentx-wc-iframe",
    "attributes": {
        "src": "https://widget.example.com/embedded-app"
    },
    "wrapper": {
        "title": "AgentX iFrame",
        "maximizeAreaName": "app-maximize-area"
    },
    "style": {
        "height": "504px",
        "width": "520px",
        "display": "inline-block",
        "align-items": "center"
    }
}
```

Step 6: Use the `attributes` property tag to add iFrame attributes.

```json
{
    "comp": "agentx-wc-iframe",
    "attributes": {
        "src": "https://widget.example.com/embedded-app",
        "sandbox": "allow-scripts allow-popups"
    },
    "wrapper": {
        "title": "AgentX iFrame",
        "maximizeAreaName": "app-maximize-area"
    },
    "style": {
        "height": "504px",
        "width": "520px",
        "display": "inline-block",
        "align-items": "center"
    }
}
```
