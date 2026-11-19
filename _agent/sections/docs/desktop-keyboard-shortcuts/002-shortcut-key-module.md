---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-keyboard-shortcuts
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Shortcut Key Module
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/desktop-keyboard-shortcuts). [Full Markdown](../../../../docs/desktop-keyboard-shortcuts.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before You Begin](001-before-you-begin.md)

## Article introduction

Register, inspect, and remove keyboard shortcuts, and handle key presses and conflicts in Desktop widgets.

## Selected section

## Shortcut Key Module

The `Desktop.shortcutKey` module registers shortcut actions and listens for shortcut events. Check both `DEFAULT_SHORTCUT_KEYS` and `getRegisteredKeys()` before selecting a key combination; another widget may have registered it. You must know the list of existing shortcut keys in Desktop to avoid conflicts. For more information, see the [Access Keyboard Shortcuts](https://www.cisco.com/c/en/us/td/docs/voice_ip_comm/cust_contact/contact_center/webexcc/desktop_20/webexcc_b_20-desktop-user-guide/webexcc_b_30-cisco-webex-contact-center-agent_chapter_00.html#Cisco_Task_in_List_GUI.dita_60eba694-3011-42b5-9bfc-ec737a82315e) section in the _Introduction_ chapter of the _Cisco Webex Contact Center Agent Desktop User Guide_.

**Example**

```javascript
import {
    Desktop
} from "@wxcc-desktop/sdk";

console.log(Desktop.shortcutKey.DEFAULT_SHORTCUT_KEYS); //=> logs default shortcut keys

console.log(Desktop.shortcutKey.MODIFIERS); //=> logs keys modifiers

console.log(Desktop.shortcutKey.REGISTERED_KEYS); //=> logs registered keys without modifiers

console.log(Desktop.shortcutKey.getRegisteredKeys()); //=> logs service registered keys with modifiers (full information)

Desktop.shortcutKey.listenKeyPress((event) => {
// Other widget setup omitted.
}); //=> listen shortcuts key press

Desktop.shortcutKey.listenKeyConflict((event) => {
// Other widget setup omitted.
}); //=> listen shortcuts key conflict

Desktop.shortcutKey.listenConflictResolved(() => {}); //=> listen to shortcut key conflict resolved status

// See register() below for a complete shortcut definition.


Desktop.shortcutKey.unregisterKeys('widget-one-example'); //=> used to unregister on unmount, widgetElement used for register should be provided
```

### Methods

#### register()

Registers the shortcut key actions.

**Example**

```javascript
Desktop.shortcutKey.register([
  {
    componentName: "Sample Comp",
    actionName: "login",
    modifierKeys: "ctrlKey_altKey",
    key: "j",
    callback: (data) => {}
  }
]);
```

The following table lists the payload details:

| Name          | Type     | Description                                                                                                                                                                                                                                                                                                      | Required |
| ------------- | -------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- |
| componentName | String   | The name of the functionality, component, or the widget.                                                                                                                                                                                                                                                         | Yes      |
| actionName    | String   | Name of the action or operation performed by the assigned shortcut keys.                                                                                                                                                                                                                                         | Yes      |
| modifierKeys  | String   | The modifier key is used commonly in keyboard shortcuts on the host platform. The keyboard modifier key combinations are:<br>- Ctrl + Shift<br>- Alt + Shift<br>- Ctrl + Alt<br>- Shift<br>- Ctrl<br>- Alt                                                                                                       | Yes      |
| key           | String   | The main key to be combined with modifier keys. For example, Ctrl + Shift + e where Ctrl and Shift are the modifier keys, and e is the main key.                                                                                                                                                                 | Yes      |
| callback      | Function | Client code can add the callback function while registering the shortcut key. When the shortcut key framework finds the matching keys from the registered keys list on the keyboard `keyup` event, then the shortcut framework invokes the callback method. The `keyup` event is invoked when a key is released. | Yes      |

**Returns**

`{void}` Registers the shortcuts; no value is returned.

**Example Registered Key Data**

```javascript
const register = [
        {
            "widgetElement": "agentx-wc-navigation",
            "group": "Navigation",
            "action": "Open Home Page",
            "modifierKeys": "ctrlKey_altKey",
            "key": "1"
        },
        // widgetElement is the name of the web component
        // group is the name of the functionality, component, or the widget.
        {
            "widgetElement": "agentx-wc-navigation",
            "group": "Navigation",
            "action": "Open Agent Performance Statistics Page",
            "modifierKeys": "ctrlKey_altKey",
            "key": "2"
        },
        {
            "widgetElement": "agentx-wc-navigation",
            "group": "Navigation",
            "action": "Open Widget Using JS API Page",
            "modifierKeys": "ctrlKey_altKey",
            "key": "3"
        }
];
```

#### getRegisteredKeys()

Retrieves the registered shortcut keys with the modifiers.

**Example**

```javascript
console.log(Desktop.shortcutKey.getRegisteredKeys());
```

**Returns**
`{Map | undefined}` A map of registered key identifiers to key information. It is undefined when the service is unavailable.

**Example Response**

```javascript
const getRegisteredKeys = new Map([
  [
    "Go to Available StatectrlKey_altKeyr",
    {
      widgetElement: "agentx-react-state-selector",
      group: "Agent State",
      action: "Go to Available State",
      modifierKeys: "ctrlKey_altKey",
      key: "r"
    }
  ],
  [
    "Go to Idle StatectrlKey_altKeyn",
    {
      widgetElement: "agentx-react-state-selector",
      group: "Agent State",
      action: "Go to Idle State",
      modifierKeys: "ctrlKey_altKey",
      key: "n"
    }
  ],
  [
    "Send EmailctrlKey_altKeys",
    {
      widgetElement: "agentx-react-email-composer",
      group: "Email Handling",
      action: "Send Email",
      modifierKeys: "ctrlKey_altKey",
      key: "s"
    }
  ],
  [
    "ReplyctrlKey_shiftKey6",
    {
      widgetElement: "agentx-react-email-composer",
      group: "Email Handling",
      action: "Reply",
      modifierKeys: "ctrlKey_shiftKey",
      key: "6"
    }
  ],
  [
    "Reply AllctrlKey_shiftKey5",
    {
      widgetElement: "agentx-react-email-composer",
      group: "Email Handling",
      action: "Reply All",
      modifierKeys: "ctrlKey_shiftKey",
      key: "5"
    }
  ],
  [
    "Open Outbound callctrlKey_altKeyo",
    {
      widgetElement: "agentx-react-out-dial",
      group: "Outbound",
      action: "Open Outbound call",
      modifierKeys: "ctrlKey_altKey",
      key: "o"
    }
  ],
  [
    "Open Notification CenterctrlKey_altKeyi",
    {
      widgetElement: "wagentx-wc-menu-notification",
      group: "Notification",
      action: "Open Notification Center",
      modifierKeys: "ctrlKey_altKey",
      key: "i"
    }
  ],
  [
    "Enable Silent NotificationsctrlKey_altKeyd",
    {
      widgetElement: "wagentx-wc-menu-notification",
      group: "Notification",
      action: "Enable Silent Notifications",
      modifierKeys: "ctrlKey_altKey",
      key: "d"
    }
  ],
  [
    "Accept Chat/Email/SocialctrlKey_altKeya",
    {
      widgetElement: "agentx-react-interaction-control",
      group: "Application",
      action: "Accept Chat/Email/Social",
      modifierKeys: "ctrlKey_altKey",
      key: "a"
    }
  ],
  [
    "Switch between PopoversctrlKey_altKeyp",
    {
      widgetElement: "agentx-react-interaction-control",
      group: "Application",
      action: "Switch between Popovers",
      modifierKeys: "ctrlKey_altKey",
      key: "p"
    }
  ],
  [
    "Expand/Collapse the PopoverctrlKey_shiftKey9",
    {
      widgetElement: "agentx-react-interaction-control",
      group: "Application",
      action: "Expand/Collapse the Popover",
      modifierKeys: "ctrlKey_shiftKey",
      key: "9"
    }
  ],
  [
    "Accept all (visible) PopoversctrlKey_shiftKey4",
    {
      widgetElement: "agentx-react-interaction-control",
      group: "Application",
      action: "Accept all (visible) Popovers",
      modifierKeys: "ctrlKey_shiftKey",
      key: "4"
    }
  ],
  [
    "Hold/Resume CallctrlKey_altKeyv",
    {
      widgetElement: "agentx-react-interaction-control",
      group: "Interaction Control",
      action: "Hold/Resume Call",
      modifierKeys: "ctrlKey_altKey",
      key: "v"
    }
  ],
  [
    "Pause/Resume RecordingctrlKey_shiftKeyz",
    {
      widgetElement: "agentx-react-interaction-control",
      group: "Interaction Control",
      action: "Pause/Resume Recording",
      modifierKeys: "ctrlKey_shiftKey",
      key: "z"
    }
  ],
  [
    "Conference Request for Call/ChatctrlKey_altKeyh",
    {
      widgetElement: "agentx-react-interaction-control",
      group: "Interaction Control",
      action: "Conference Request for Call/Chat",
      modifierKeys: "ctrlKey_altKey",
      key: "h"
    }
  ],
  [
    "Consult Request for CallctrlKey_altKeyc",
    {
      widgetElement: "agentx-react-interaction-control",
      group: "Interaction Control",
      action: "Consult Request for Call",
      modifierKeys: "ctrlKey_altKey",
      key: "c"
    }
  ],
  [
    "End for All ChannelsctrlKey_altKeye",
    {
      widgetElement: "agentx-react-interaction-control",
      group: "Interaction Control",
      action: "End for All Channels",
      modifierKeys: "ctrlKey_altKey",
      key: "e"
    }
  ],
  [
    "Transfer Request for All ChannelsctrlKey_altKeyx",
    {
      widgetElement: "agentx-react-interaction-control",
      group: "Interaction Control",
      action: "Transfer Request for All Channels",
      modifierKeys: "ctrlKey_altKey",
      key: "x"
    }
  ],
  [
    "Save Edited CAD Variable ValuesctrlKey_altKeym",
    {
      widgetElement: "agentx-react-interaction-control",
      group: "Interaction Control",
      action: "Save Edited CAD Variable Values",
      modifierKeys: "ctrlKey_altKey",
      key: "m"
    }
  ],
  [
    "Revert Edited CAD Variable ValuesctrlKey_altKeyz",
    {
      widgetElement: "agentx-react-interaction-control",
      group: "Interaction Control",
      action: "Revert Edited CAD Variable Values",
      modifierKeys: "ctrlKey_altKey",
      key: "z"
    }
  ],
  [
    "Expand/CollapsectrlKey_shiftKeyy",
    {
      widgetElement: "agentx-react-interaction-control",
      group: "Interaction Control",
      action: "Expand/Collapse",
      modifierKeys: "ctrlKey_shiftKey",
      key: "y"
    }
  ],
  [
    "Wrap Up ReasonctrlKey_altKeyw",
    {
      widgetElement: "agentx-react-interaction-control",
      group: "Interaction Control",
      action: "Wrap Up Reason",
      modifierKeys: "ctrlKey_altKey",
      key: "w"
    }
  ],
  [
    "Open User ProfilectrlKey_altKeyu",
    {
      widgetElement: "agentx-react-agent-profile",
      group: "User Profile",
      action: "Open User Profile",
      modifierKeys: "ctrlKey_altKey",
      key: "u"
    }
  ],
  [
    "Sign OutctrlKey_altKeyl",
    {
      widgetElement: "agentx-react-agent-profile",
      group: "User Profile",
      action: "Sign Out",
      modifierKeys: "ctrlKey_altKey",
      key: "l"
    }
  ],
  [
    "Open Keyboard Shortcuts ListctrlKey_altKeyf",
    {
      widgetElement: "agentx-react-agent-profile",
      group: "User Profile",
      action: "Open Keyboard Shortcuts List",
      modifierKeys: "ctrlKey_altKey",
      key: "f"
    }
  ],
  [
    "Download Error ReportctrlKey_shiftKey2",
    {
      widgetElement: "agentx-react-agent-profile",
      group: "User Profile",
      action: "Download Error Report",
      modifierKeys: "ctrlKey_shiftKey",
      key: "2"
    }
  ],
  [
    "Switch between active tasksctrlKey_shiftKey8",
    {
      widgetElement: "agentx-wc-task-list",
      group: "Task List",
      action: "Switch between active tasks",
      modifierKeys: "ctrlKey_shiftKey",
      key: "8"
    }
  ],
  [
    "Expand/Collapse the Task PanelctrlKey_shiftKey7",
    {
      widgetElement: "agentx-wc-task-list",
      group: "Task List",
      action: "Expand/Collapse the Task Panel",
      modifierKeys: "ctrlKey_shiftKey",
      key: "7"
    }
  ],
  [
    "Open Navigation TabctrlKey_altKeyt",
    {
      widgetElement: "agentx-wc-connector",
      group: "Connector View",
      action: "Open Navigation Tab",
      modifierKeys: "ctrlKey_altKey",
      key: "t"
    }
  ],
  [
    "RefreshctrlKey_altKeyb",
    {
      widgetElement: "agentx-wc-connector",
      group: "Connector View",
      action: "Refresh",
      modifierKeys: "ctrlKey_altKey",
      key: "b"
    }
  ],
  [
    "Open HomectrlKey_altKey1",
    {
      widgetElement: "agentx-wc-navigation",
      group: "Navigation",
      action: "Open Home",
      modifierKeys: "ctrlKey_altKey",
      key: "1"
    }
  ],
  [
    "Open Agent Performance StatisticsctrlKey_altKey2",
    {
      widgetElement: "agentx-wc-navigation",
      group: "Navigation",
      action: "Open Agent Performance Statistics",
      modifierKeys: "ctrlKey_altKey",
      key: "2"
    }
  ],
  [
    "Open Webex Experience Manager MetricsctrlKey_altKey3",
    {
      widgetElement: "agentx-wc-navigation",
      group: "Navigation",
      action: "Open Webex Experience Manager Metrics",
      modifierKeys: "ctrlKey_altKey",
      key: "3"
    }
  ]
]);
```

#### Default Shortcut Keys

Logs the default shortcut keys.

**Example**

```javascript
console.log(Desktop.shortcutKey.DEFAULT_SHORTCUT_KEYS);
```

**Returns**
`{Object | undefined}` An object keyed by shortcut group; each group contains an array of key information. It is undefined when the service is unavailable.

**Example Response**

```javascript
const DEFAULT_SHORTCUT_KEYS = {
  agentState: [
    {
      widgetElement: "agentx-react-state-selector",
      group: "Agent State",
      action: "Go to Available State",
      modifierKeys: "ctrlKey_altKey",
      key: "r"
    },
    {
      widgetElement: "agentx-react-state-selector",
      group: "Agent State",
      action: "Go to Idle State",
      modifierKeys: "ctrlKey_altKey",
      key: "n"
    }
  ],
  emailComposer: [
    {
      widgetElement: "agentx-react-email-composer",
      group: "Email Handling",
      action: "Send Email",
      modifierKeys: "ctrlKey_altKey",
      key: "s"
    },
    {
      widgetElement: "agentx-react-email-composer",
      group: "Email Handling",
      action: "Reply",
      modifierKeys: "ctrlKey_shiftKey",
      key: "6"
    },
    {
      widgetElement: "agentx-react-email-composer",
      group: "Email Handling",
      action: "Reply All",
      modifierKeys: "ctrlKey_shiftKey",
      key: "5"
    }
  ],
  outDial: [
    {
      widgetElement: "agentx-react-out-dial",
      group: "Outbound",
      action: "Open Outbound call",
      modifierKeys: "ctrlKey_altKey",
      key: "o"
    }
  ],
  notification: [
    {
      widgetElement: "wagentx-wc-menu-notification",
      group: "Notification",
      action: "Open Notification Center",
      modifierKeys: "ctrlKey_altKey",
      key: "i"
    },
    {
      widgetElement: "wagentx-wc-menu-notification",
      group: "Notification",
      action: "Enable Silent Notifications",
      modifierKeys: "ctrlKey_altKey",
      key: "d"
    }
  ],
  interactionPopover: [
    {
      widgetElement: "agentx-react-interaction-control",
      group: "Application",
      action: "Accept Chat/Email/Social",
      modifierKeys: "ctrlKey_altKey",
      key: "a"
    },
    {
      widgetElement: "agentx-react-interaction-control",
      group: "Application",
      action: "Switch between Popovers",
      modifierKeys: "ctrlKey_altKey",
      key: "p"
    },
    {
      widgetElement: "agentx-react-interaction-control",
      group: "Application",
      action: "Expand/Collapse the Popover",
      modifierKeys: "ctrlKey_shiftKey",
      key: "9"
    },
    {
      widgetElement: "agentx-react-interaction-control",
      group: "Application",
      action: "Accept all (visible) Popovers",
      modifierKeys: "ctrlKey_shiftKey",
      key: "4"
    }
  ],
  interactionControl: [
    {
      widgetElement: "agentx-react-interaction-control",
      group: "Interaction Control",
      action: "Hold/Resume Call",
      modifierKeys: "ctrlKey_altKey",
      key: "v"
    },
    {
      widgetElement: "agentx-react-interaction-control",
      group: "Interaction Control",
      action: "Pause/Resume Recording",
      modifierKeys: "ctrlKey_shiftKey",
      key: "z"
    },
    {
      widgetElement: "agentx-react-interaction-control",
      group: "Interaction Control",
      action: "Conference Request for Call/Chat",
      modifierKeys: "ctrlKey_altKey",
      key: "h"
    },
    {
      widgetElement: "agentx-react-interaction-control",
      group: "Interaction Control",
      action: "Consult Request for Call",
      modifierKeys: "ctrlKey_altKey",
      key: "c"
    },
    {
      widgetElement: "agentx-react-interaction-control",
      group: "Interaction Control",
      action: "End for All Channels",
      modifierKeys: "ctrlKey_altKey",
      key: "e"
    },
    {
      widgetElement: "agentx-react-interaction-control",
      group: "Interaction Control",
      action: "Transfer Request for All Channels",
      modifierKeys: "ctrlKey_altKey",
      key: "x"
    },
    {
      widgetElement: "agentx-react-interaction-control",
      group: "Interaction Control",
      action: "Save Edited CAD Variable Values",
      modifierKeys: "ctrlKey_altKey",
      key: "m"
    },
    {
      widgetElement: "agentx-react-interaction-control",
      group: "Interaction Control",
      action: "Revert Edited CAD Variable Values",
      modifierKeys: "ctrlKey_altKey",
      key: "z"
    },
    {
      widgetElement: "agentx-react-interaction-control",
      group: "Interaction Control",
      action: "Expand/Collapse",
      modifierKeys: "ctrlKey_shiftKey",
      key: "y"
    },
    {
      widgetElement: "agentx-react-interaction-control",
      group: "Interaction Control",
      action: "Wrap Up Reason",
      modifierKeys: "ctrlKey_altKey",
      key: "w"
    }
  ],
  userProfile: [
    {
      widgetElement: "agentx-react-agent-profile",
      group: "User Profile",
      action: "Open User Profile",
      modifierKeys: "ctrlKey_altKey",
      key: "u"
    },
    {
      widgetElement: "agentx-react-agent-profile",
      group: "User Profile",
      action: "Sign Out",
      modifierKeys: "ctrlKey_altKey",
      key: "l"
    },
    {
      widgetElement: "agentx-react-agent-profile",
      group: "User Profile",
      action: "Open Keyboard Shortcuts List",
      modifierKeys: "ctrlKey_altKey",
      key: "f"
    },
    {
      widgetElement: "agentx-react-agent-profile",
      group: "User Profile",
      action: "Download Error Report",
      modifierKeys: "ctrlKey_shiftKey",
      key: "2"
    }
  ],
  taskList: [
    {
      widgetElement: "agentx-wc-task-list",
      group: "Task List",
      action: "Switch between active tasks",
      modifierKeys: "ctrlKey_shiftKey",
      key: "8"
    },
    {
      widgetElement: "agentx-wc-task-list",
      group: "Task List",
      action: "Expand/Collapse the Task Panel",
      modifierKeys: "ctrlKey_shiftKey",
      key: "7"
    }
  ],
  connectorView: [
    {
      widgetElement: "agentx-wc-connector",
      group: "Connector View",
      action: "Open Navigation Tab",
      modifierKeys: "ctrlKey_altKey",
      key: "t"
    },
    {
      widgetElement: "agentx-wc-connector",
      group: "Connector View",
      action: "Refresh",
      modifierKeys: "ctrlKey_altKey",
      key: "b"
    }
  ]
};
```

#### Modifiers

Logs the shortcut key modifier. A modifier shortcut key is Shift, Ctrl, Alt, or a combination of these keys.

**Example**

```javascript
console.log(Desktop.shortcutKey.MODIFIERS);
```

**Returns**
`{Object}` The object response.

**Example Response**

```javascript
const MODIFIERS = {
  CTRL_SHIFT: "ctrlKey_shiftKey",
  ALT_SHIFT: "altKey_shiftKey",
  CTRL_ALT: "ctrlKey_altKey",
  SHIFT: "shiftKey",
  CTRL: "ctrlKey",
  ALT: "altKey"
};
```

#### Registered Keys

Logs registered shortcut keys without the modifiers.

**Example**

```javascript
console.log(Desktop.shortcutKey.REGISTERED_KEYS);
```

**Returns**
`{Object}` The object response.

**Example Response**

```javascript
const REGISTERED_KEYS = {
  EXPAND_COLLAPSE_INTERACTION_PANEL_KEY: "y",
  SAVE_EDITED_CAD_KEY: "m",
  REVERT_EDITED_CAD_KEY: "z",
  HOLD_RESUME_CALL_KEY: "v",
  TRANSFER_KEY: "x",
  CONSULT_KEY: "c",
  END_KEY: "e",
  CONFERENCE_KEY: "h",
  PAUSE_RESUME_RECORDING_KEY: "z",
  GO_TO_AVAILABLE_KEY: "r",
  OPEN_STATE_SELECTOR_KEY: "n",
  SEND_EMAIL_KEY: "s",
  REPLY_EMAIL_KEY: "6",
  REPLY_ALL_EMAIL_KEY: "5",
  OPEN_USER_PROFILE_KEY: "u",
  ENABLE_SILENT_NOTIFICATION_KEY: "d",
  OPEN_SHORTCUT_KEY_MODAL_KEY: "f",
  DOWNLOAD_ERROR_REPORT_KEY: "2",
  SIGNOUT_KEY: "l",
  ACCEPT_TASK_KEY: "a",
  SWITCH_POPOVER_KEY: "p",
  EXPAND_COLLAPSE_POPOVER_KEY: "9",
  OPEN_OUTDIAL_KEY: "o",
  OPEN_WRAP_UP_KEY: "w",
  EXPAND_COLLAPSE_TASK_LIST_PANEL_KEY: "7",
  OPEN_NOTIFICATION_CENTER_KEY: "i",
  OPEN_NAVIGATION_TAB_KEY: "t",
  REFRESH_KEY: "b",
  SWITCH_TASK_KEY: "8",
  ACCEPT_ALL_TASK_KEY: "4"
};
```

#### unregisterKeys()

Unregisters the shortcut keys.

**Example**

```javascript
Desktop.shortcutKey.unregisterKeys("custom-element");
```

**Parameters**

| Name | Type | Description | Required |
| --- | --- | --- | --- |
| widgetElement | String | The widget element name used to register its shortcuts. Removes that widget's shortcuts during unmount. | Yes |

#### listenKeyPress(callback)

Listens to shortcut key press.

**Example**

```javascript
Desktop.shortcutKey.listenKeyPress((event) => {
  console.log("JSSDK ShortcutKey listenKeyPress: ", event);
});
```

**Parameters**

| Name  | Type   | Description                                       | Required |
| ----- | ------ | ------------------------------------------------- | -------- |
| callback | Function | Receives the shortcut event when a keyboard key is released. | Yes |

**Callback payload**
`{Object}` The shortcut event passed to the callback.

**Example Callback Payload**

```json
{
  "type": "execute",
  "data": {
    "widgetElement": "agentx-react-agent-profile",
    "group": "User Profile",
    "action": "Open Keyboard Shortcuts List",
    "modifierKeys": "ctrlKey_altKey",
    "key": "f",
    "keyCombination": "Ctrl + Alt + F"
  },
  "keyboardEvent": {
    "isTrusted": true
  }
}
```

#### listenKeyConflict(callback)

Listens to shortcut key conflicts.

**Example**

```javascript
Desktop.shortcutKey.listenKeyConflict((event) => {
            console.log("JSSDK ShortcutKey listenKeyPress: ", event);
        });
```

**Parameters**

| Name  | Type   | Description                                       | Required |
| ----- | ------ | ------------------------------------------------- | -------- |
| callback | Function | Receives the shortcut event when a keyboard key is released. | Yes |

**Callback payload**
`{Object}` The shortcut event passed to the callback.

**Example Callback Payload**

```json
{
    "type": "conflict",
    "data": {
        "widgetElement": "agentx-react-agent-profile",
        "group": "User Profile",
        "action": "Open Keyboard Shortcuts List",
        "modifierKeys": "ctrlKey_altKey",
        "key": "f",
        "isConflict": true
    }
}
```

#### listenConflictResolved(callback)

Registers a callback invoked when a shortcut key conflict is resolved.

**Example**

```javascript
Desktop.shortcutKey.listenConflictResolved(() => {});
```
