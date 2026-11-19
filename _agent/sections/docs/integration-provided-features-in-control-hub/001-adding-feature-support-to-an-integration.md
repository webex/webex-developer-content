---
type: Excerpt
canonical_url: https://developer.webex.com/docs/integration-provided-features-in-control-hub
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Adding feature support to an integration
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/integration-provided-features-in-control-hub). [Full Markdown](../../../../docs/integration-provided-features-in-control-hub.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Workspace integrations can also provide new functionality in Control Hub. To achieve this, integrations can mark themselves as providing **features**, which are contracts integrations can specify that they support. Integrations that provide features are highlighted on the integrations page, and when activated, they enhance functionality provided in other areas of Control Hub.

---

Control Hub supports integration-provided digital signage and Room Navigator persistent web apps. When an integration that is marked as providing digital signage is enabled, it's available as a service in the bulk and single-device digital signage configuration modals. Read more about configuring digital signage on Webex Boards, Room, and Desk series devices [here](https://help.webex.com/en-us/article/nmd8log/Enable-Digital-Signage-on-Webex-Boards,-Room,-and-Desk-Series-Devices). Similarly, integrations providing Room Navigator persistent web apps appear in the persistent web app configuration modals. Learn how to configure a persistent web app on a Room Navigator device [here](https://help.webex.com/en-us/article/ohq3u6/Configure-a-persistent-web-app-on-Webex-Room-Navigator).

## Selected section

## Adding feature support to an integration

To register an integration as providing a feature, a new `features` list must be added to the manifest. Adding a feature to this list places requirements on what information it must provide and the actions it needs to support.

Providing features may also require specific permissions. Digital signage requires the `spark-admin:devices_digital_signage` scope and persistent web apps require the `spark-admin:devices_pwa` scope.

**Example**

```json
{
  "apiAccess": [
    {
      "scope": "spark-admin:devices_digital_signage",
      "access": "required"
    },
    {
      "scope": "spark-admin:devices_pwa",
      "access": "required"
    }
  ],
  "features": ["digital_signage", "persistent_web_app"]
  // ...
}
```

**Manifest Details**



| Field | Required / Optional | Value space | Description |
| ----- | ------------------- | ----------- |------------ |
| `features` | Optional | Array | The list of features supported: `digital_signage`, `persistent_web_app` |

Attention: Adding a feature to the manifest grants the integration access to new management APIs. An integration providing digital signage or persistent web apps is not fully provisioned until it uses the corresponding feature's management API to provide a configuration object. Integrations should upload configurations for the features they provide shortly after being provisioned. If a feature is added to an existing manifest, ensure that configurations are provided to existing installations by listening for the `updateApproved` action. Consider adding a periodic check to your integration verifying the feature configurations, in case of failures when storing the configurations or lost `updateApproved` actions.
