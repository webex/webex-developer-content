---
type: Excerpt
canonical_url: https://developer.webex.com/docs/devices
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Device Configurations and xAPI Reference Guide
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/devices). [Full Markdown](../../../../docs/devices.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Provision, manage and control your Webex devices.

---

An integrator can use the device APIs to integrate with devices. There are four APIs that can be used to interact with devices:

- **[Devices API](https://developer.webex.com/docs/devices#devices-api)**: The inventory of your devices that can be used to view and delete devices or to create activation codes for getting new devices online.
- **[Device Configurations API](https://developer.webex.com/docs/devices#device-configurations-api)**: View and update the configurations of any device, online or offline.
- **[Workspaces API](https://developer.webex.com/docs/devices#workspaces-api)**: Create, view, update and delete workspaces. Workspaces represent where people work, such as conference rooms and meeting spaces
- **[xAPI](https://developer.webex.com/docs/devices#xapi)**: Allows developers to programmatically invoke commands and query the status of devices.

## Selected section

## Device Configurations and xAPI Reference Guide

Descriptions of the configurations and the xAPI commands and statuses are in the [Cisco Collaboration Endpoint Software API Reference Guide](https://www.cisco.com/c/en/us/support/collaboration-endpoints/spark-room-kit-series/products-command-reference-list.html) – look for the newest version. The API Reference Guide uses the *terminal mode notation* for commands and statuses. As explained in the previous sections, its easy to translate from terminal mode to the JSON based Webex API format.

### Terminal mode notation

```text
xConfig <path> <key>: <value> <key>: <value>
xCommand <path> <key>: <value> <key>: <value>
xStatus <path>
```

- Prefix: **xConfiguration** for configurations; **xCommand** for commands; **xStatus** for statuses.
- Path: Space-separated segments that form the full path of the configuration, command or status.
- Arguments: Zero or more key-value pairs. The key and value are separated by colon (": "). Applies only to configurations and commands; statuses don't have arguments.

Examples:

```text
xConfiguration Audio DefaultVolume: 10
xCommand Audio Volume Increase Steps: 5
xStatus Audio Volume
```
