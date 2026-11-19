---
type: Guide
title: Notifications and Screen Pops
display_title: Notifications and Screen Pops
canonical_url: https://developer.webex.com/docs/desktop-notifications-screen-pops
content_type: documentation
product_group:
- webex-contact-center
categories:
- webex-contact-center
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/desktop-notifications-screen-pops)

Send Desktop notifications and listen for screen-pop events from custom widgets.

## Before You Begin

Install and initialize the SDK as described in [Get Started with the Desktop SDK](https://developer.webex.com/docs/desktop-sdk-getting-started). Your widget must run inside Webex Contact Center Desktop.

## Desktop Actions

The `Desktop.actions` module retrieves data and performs actions for Desktop widgets.

### fireGeneralSilentNotification(raw)

Triggers silent notifications. Silent notifications do not appear on the desktop, but are listed in the Notification Center. The **Notification Center** icon indicates the increase in the number of unread messages.

**Note:** You can customize the notification icon displayed in the Notification Center dialog box using the iconDetail object.

**Example**

```typescript
import {
    Desktop
} from "@wxcc-desktop/sdk";
import {
    Notifications,
    NotificationItemsContent
} from "@uuip/unified-ui-platform-sdk";


const raw: Notifications.ItemMeta.Raw = {
    data: {
        type: Notifications.ItemMeta.Type.Info,
        mode: Notifications.ItemMeta.Mode.Silent, // Change type here based on the method.
        title: "Info - Silent",
        data: new NotificationItemsContent.DataController({
            text: "Explore New Horizons",
            link: "https://www.abc.com/file/Tjpn4Z9p8jZy0Da0Ggq6ra/Priority-To-do-list?node-id=1280%3A83124",
            linkName: 'Toaster Notification',
            linkTooltip: `<div style="text-align: left !important;">Phone - +1 (412)555-3782 <br /> Queue - IVR_Queue <br /> Activity Label <br /> URL - www.google.com <br /> Phone - +1-408-000-0001 <br /> Account - 81684989000 </div>`,
            iconDetail: {
                iconName: 'icon-alert-active_16',
                color: 'blue',
                iconColor: '#08599C'
            },
            actions: [
              {
                label: "Yes",
                handler: n => {
                  console.log("Yes button clicked", n);
                },
                variant: "primary"
              },
              {
                label: "No",
                handler: n => {
                  console.log("No button clicked", n);
                },
                variant: "secondary"
              }
            ],
        })
    },
};

// Desktop General Notifications:
Desktop.actions.fireGeneralSilentNotification(raw)
// => Fires silent notification in Desktop.
// Silent notification will not have any apperance on desktop but a notification icon will have one count increased.
```

**Parameters**

| Name            | Type     | Description                                                                                                                                                                                                                                                   | Required |
| --------------- | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- |
| raw             | Object   | Contains information regarding the type of notification sent to the user.                                                                                                                                                                                     | Yes      |
| -->data         | Object   | Options of the specific notification.                                                                                                                                                                                                                         | Yes      |
| --> type        | Enum     | The type of notifications displayed on the Desktop. (Info, Warn, Error, Success, Chat, Default)                                                                                                                                                               | Yes      |
| -->mode         | Enum     | The available mode of notification based on the method. (Silent, AutoDismiss, Acknowledge)                                                                                                                                                                    | Yes      |
| -->title        | String   | The title of the notification.                                                                                                                                                                                                                                | Yes      |
| -->data         | Object   | Options for the notification content.                                                                                                                                                                                                                         | Yes      |
| --> type        | String   | The media channel type such as chat and social.                                                                                                                                                                                                               | Optional |
| -->text         | String   | The subheading of the notification.                                                                                                                                                                                                                           | Yes      |
| -->link         | String   | The link address to the notification.                                                                                                                                                                                                                         | Optional |
| -->linkName     | String   | The text to display for the link.                                                                                                                                                                                                                             | Optional |
| -->linkTooltip  | String   | The tooltip for the link.                                                                                                                                                                                                                                     | Optional |
| -->iconDetail   | Object   | Custom details for the notification icon.                                                                                                                                                                                                                     | Optional |
| -->iconName     | String   | Name of the notification icon.                                                                                                                                                                                                                                | Yes      |
| -->color        | String   | The color of the circle in the background, in which the notification icon is placed. This color changes based on the light mode or dark mode selection.                                                                                                       | Optional |
| -->bgColor      | String   | The color of the circle in the background, in which the notification icon is placed. This color does not change based on the light mode or dark mode selection. <br>**Note:** If both the `color` and `bgColor` are defined, then `bgColor` takes precedence. | Optional |
| -->iconColor    | String   | The color of the notification icon.                                                                                                                                                                                                                           | Optional |
| -->linkHandler  | Function | The function that is invoked when the conditions are met.                                                                                                                                                                                                     | Optional |
| -->errorDetail  | Object   | Options for the notification error.                                                                                                                                                                                                                           | Optional |
| -->header       | String   | The title of the notification error.                                                                                                                                                                                                                          | Optional |
| -- >message     | String   | The message displayed in the notification error modal dialog.                                                                                                                                                                                                 | Yes      |
| -->trackingId   | String   | Unique identifier based on the notification error.                                                                                                                                                                                                            | Optional |
| -->localization | Object   | Options for the localization (i18n) module.                                                                                                                                                                                                                   | Yes      |
| -- >timestamp   | String   | The time at which the notification error was generated. Timestamp uses the format `DateTime.fromMillis (now + 4).to ISO()`.                                                                                                                                   | Optional |
| -->taskId       | String   | Unique identifier for the task.                                                                                                                                                                                                                               | Optional |
| -->dismissHandler | Function | The function invoked when the notification is dismissed.                                                                | Optional |
| -->actions        | Array    | The actions supported by the notification. These are rendered as buttons that can be used to process different types of responses from the user e.g. Accept/Decline, Yes/No/Later etc. For more information, see Action.                                                                                   | Optional |
| -->lineClamp | Number | Maximum number of lines from the `message` displayed on the notification before truncation.                                                    | Optional |

**Action**

| Name    | Type     | Description                                                                                                                         |
| ------- | -------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| label   | String   | The text displayed on the action button.                                                                                            |
| variant | String   | The variant of the action button. Determines the look of the button. See the Button component under the Momentum UI Web Component Library for the available variants. |
| handler | Function | The function invoked when the button is clicked.                                                                                    |

### fireGeneralAutoDismissNotification(raw)

Triggers the auto-dismiss notification. Returns the notification resolved status, reason, and mode.

**Note:** If Desktop notifications are disabled by the user, they are converted into silent notifications and reflected in mode.

**Example**

```typescript
import {
    Desktop
} from "@wxcc-desktop/sdk";
import {
    Notifications,
    NotificationItemsContent
} from "@uuip/unified-ui-platform-sdk";


const raw: Notifications.ItemMeta.Raw = {
    data: {
        type: Notifications.ItemMeta.Type.Info,
        mode: Notifications.ItemMeta.Mode.AutoDismiss, // Change type here based on the method.
        title: "Info - AutoDismiss",
        data: new NotificationItemsContent.DataController({
            text: "Explore New Horizons",
            link: "https://www.abc.com/file/Tjpn4Z9p8jZy0Da0Ggq6ra/Priority-To-do-list?node-id=1280%3A83124",
            linkName: 'Toaster Notification',
            linkTooltip: `<div style="text-align: left !important;">Phone - +1 (412)555-3782 <br /> Queue - IVR_Queue <br /> Activity Label <br /> URL - www.google.com <br /> Phone - +1-408-000-0001 <br /> Account - 81684989000 </div>`,
            iconDetail: {
                iconName: 'icon-alert-active_16',
                color: 'blue',
                iconColor: '#08599C'
            }
        })
    },
};

// Unlike silent notification, auto-dismiss and acknowledge can have controlled responses, that may reflect in the notification status, e.g.:

// => Fires auto-dismiss notification in Desktop. Returns notification resolved status, reason, mode.
// Note: if Desktop notifications are disabled by the user - it will be converted into silent notification and reflected in "mode"
const result = await Desktop.actions.fireGeneralAutoDismissNotification(raw);
if (result) {
  const [status, reason, mode] = result;
  console.log(status, reason, mode);
}
```

**Parameters**

| Name | Type   | Description                                                               | Required |
| ---- | ------ | ------------------------------------------------------------------------- | -------- |
| raw  | Object | Contains information regarding the type of notification sent to the user. | Yes      |

For information on more parameters used in this method, see the Parameters table of the [fireGeneralSilentNotification(raw)](https://developer.webex.com/docs/desktop-notifications-screen-pops#firegeneralsilentnotificationraw) method.

### fireGeneralAcknowledgeNotification(raw)

Triggers the acknowledge notification. Returns the notification resolved status, reason, and mode.

**Note:** If Desktop notifications are disabled by the user, they are converted into silent notifications and reflected in mode.

**Example**

```typescript
import {
    Desktop
} from "@wxcc-desktop/sdk";
import {
    Notifications,
    NotificationItemsContent
} from "@uuip/unified-ui-platform-sdk";


const raw: Notifications.ItemMeta.Raw = {
    data: {
        type: Notifications.ItemMeta.Type.Info,
        mode: Notifications.ItemMeta.Mode.Acknowledge, // Change type here based on the method.
        title: "Info - Acknowledge",
        data: new NotificationItemsContent.DataController({
            text: "Explore New Horizons",
            link: "https://www.abc.com/file/Tjpn4Z9p8jZy0Da0Ggq6ra/Priority-To-do-list?node-id=1280%3A83124",
            linkName: 'Toaster Notification',
            linkTooltip: `<div style="text-align: left !important;">Phone - +1 (412)555-3782 <br /> Queue - IVR_Queue <br /> Activity Label <br /> URL - www.google.com <br /> Phone - +1-408-000-0001 <br /> Account - 81684989000 </div>`,
            iconDetail: {
                iconName: 'icon-alert-active_16',
                color: 'blue',
                iconColor: '#08599C'
            }
        })
    },
};


// => Fires acknowledge notification in Desktop. Returns notification resolved status, reason, mode.
// Note: if Desktop notifications are disabled by the user - it will be converted into silent notification and reflected in "mode"
const result = await Desktop.actions.fireGeneralAcknowledgeNotification(raw);
if (result) {
  const [status, reason, mode] = result;
  console.log(status, reason, mode);
}
```

**Parameters**

| Name | Type   | Description                                                               | Required |
| ---- | ------ | ------------------------------------------------------------------------- | -------- |
| raw  | Object | Contains information regarding the type of notification sent to the user. | Yes      |

For information on more parameters used in this method, see the Parameters table of the [fireGeneralSilentNotification(raw)](https://developer.webex.com/docs/desktop-notifications-screen-pops#firegeneralsilentnotificationraw) method.

## Screen Pop Module

The `Desktop.screenpop` module makes requests and listens to notification events related to the screen pop entity.

**Example**

```javascript
Desktop.screenpop.addEventListener("eScreenPop", (msg) => logger.info(msg));
```

To remove an event subscription in order to avoid memory leaks, you have the following options:

```javascript
// Module supports removing added listeners like:
const listener = (msg) => logger.info(msg);
Desktop.screenpop.addEventListener("eScreenPop", listener);
Desktop.screenpop.removeEventListener("eScreenPop", listener);

// Module supports one-time added listeners like:
Desktop.screenpop.addOnceEventListener("eScreenPop", listener);
Desktop.screenpop.removeOnceEventListener("eScreenPop", listener);

// Module supports removing all listeners like:
Desktop.screenpop.removeAllEventListeners();
```

### Events

#### eScreenPop

Listens to an event that displays the screen pop.

**Example**

```javascript
Desktop.screenpop.addEventListener("eScreenPop", listener);
```

**Example Response**

```javascript
const eScreenPop = {
  data: {
    agentId: "1736827c-10ef-4b2a-90e0-7d2a3743ded3",
    interactionId: "4745472e-cfa2-47f3-9fc1-16359516d648",
    queryParameters: null,
    screenPopUrl: "https://youtube.com",
    target: "insideDesktop",
    type: "ScreenPop"
  },
  orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
  trackingId: "notifs_90a4bf42-ba95-47a6-b8cb-c1ed105ff5ea",
  type: "RoutingMessage"
};
```

## Related Pages

- [Agent Desktop overview](https://developer.webex.com/docs/desktop)
- [Desktop SDK Reference](https://developer.webex.com/docs/desktop-sdk-reference)
