---
type: Guide
title: Devices | Overview
display_title: Overview
canonical_url: https://developer.webex.com/docs/devices
content_type: documentation
product_group:
- webex-suite
categories:
- devices
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/devices)

Provision, manage and control your Webex devices.

---

An integrator can use the device APIs to integrate with devices. There are four APIs that can be used to interact with devices:

- **[Devices API](https://developer.webex.com/docs/devices#devices-api)**: The inventory of your devices that can be used to view and delete devices or to create activation codes for getting new devices online.
- **[Device Configurations API](https://developer.webex.com/docs/devices#device-configurations-api)**: View and update the configurations of any device, online or offline.
- **[Workspaces API](https://developer.webex.com/docs/devices#workspaces-api)**: Create, view, update and delete workspaces. Workspaces represent where people work, such as conference rooms and meeting spaces
- **[xAPI](https://developer.webex.com/docs/devices#xapi)**: Allows developers to programmatically invoke commands and query the status of devices.

## What can I use these APIs for?

Using these APIs, you can automate things that take up a significant amount of an administrator's time every day. Think about use cases like these:

- Roll out a new setting to a group of devices with e.g. an "earlyAdopters" tag
- Generate a daily report of all devices with issues
- Make a dashboard that shows which of your devices are in use, how many are presenting content, how many people are using them and what type of workspaces they are located in
- Automatically set the type and capacity of all your workspaces based on their names
- Calculate a weekly report showing the total workspace capacity of your organization

The devices APIs expose hundreds of configurations, commands and statuses to interact with. The devices upload schema to the cloud that define the configurations, commands and statuses they support, so if a device upgrades and gets new features they are instantly available through the Device APIs.

The powerful part of this REST interface is the ability for developers and administrators to perform these actions without having direct network access to the devices, regardless of device location. This would allow them to perform actions and resolve issues on devices in home offices without physically going there. You can read and write configurations while the device is offline and any changes you make will then be applied as soon as the device comes back online. The communication channel between the REST interface and the device is encrypted.

Take a look at our [Webex Device APIs example scripts](https://github.com/CiscoDevNet/webex-device-api-examples) on Cisco DevNet for help on how to use these APIs and ideas on what to do with them. 

## Creating an application that can access the Webex REST API

In general, you can create either a [Bot](https://developer.webex.com/docs/bots) or an [Integration](https://developer.webex.com/docs/integrations). A bot cannot work across different organizations, it will only work on devices that belong to the same organization as the creator of the bot. In addition, a bot can only access devices to which it has been specifically granted access. Bots are useful for applications that are intended to be used in one organization and possibly need to be restricted to only a subset of devices. An integration, on the other hand, can perform actions on behalf of a user. Developers who wish to build applications that will work for multiple organizations, should create an integration. Administrators from multiple organizations can authorize an integration to perform actions on their behalf, and the integration will be able to access all devices in the organization(s) that the administrator(s) belong to.

The Device Configuration API and the Workspaces API are restricted to only allow administrators, not bots. That means you can try out the APIs using the [Device Configuration API Reference](https://developer.webex.com/docs/api/v1/device-configurations) and [Workspaces API Reference](https://developer.webex.com/docs/api/v1/workspaces), but in order to provide functionality for admin users to call this API you will need to create an integration that can act on behalf of them.

If you are new to creating Webex applications, check out [this blog post](https://blogs.cisco.com/developer/webex-teams-apis-awesome) to get started with REST API calls to the Webex platform.

### For Integrations

Reference the [integration documentation](https://developer.webex.com/docs/integrations) to learn how to make integrations.

In order to create an integration that can make Device API calls, your integration needs to request one or more of the following scopes:

- `spark:devices_read` - See details for your devices
- `spark:devices_write` - Modify and delete your devices
- `spark-admin:devices_read` - Read devices and device configurations in your organization
- `spark-admin:devices_write` - Create, update and delete devices and device configurations in your organization
- `spark-admin:workspaces_read` - See details for workspaces you manage.
- `spark-admin:workspaces_write` - Create, modify, and delete workspaces you manage.
- `spark:xapi_commands` - Execute commands towards devices
- `spark:xapi_statuses` - Query status on devices

### For Bots

To create a bot that can make device calls:

1. Log in to <https://developer.webex.com>, select *My Webex Apps* from the menu under your avatar at the top of this page.
2. Click *Create a New App*, followed by *Create a Bot* to start the wizard. Fill in the registration form (Bot name, Bot Username, Icon, Description), and click *Add Bot*. As the logged in user, you own the bot account, and the bot belongs to the same organization as you.
3. Copy the Access Token you receive for the new bot and keep it somewhere safe. You must always use this token to authenticate your bot with the Webex REST API. If lost, you have to generate a new one: Select *My Webex Apps* from the menu, select your bot, and click *Regenerate Access Token*.

## Giving a bot or user access to the xAPI of a device

An integration operates on behalf of a user. If this user is not an administrator of the devices in the organization, they must be explicitly granted device authorizations to the APIs just as with bots. Bots are only able to make API calls to devices which are registered in the same organization as the user who created a bot.

Your system administrator sets up device authorizations through the Cisco Webex Control Hub ([https://admin.webex.com](https://admin.webex.com)). Authorization for a bot or user is given for a *Workspace*, not a *Device*. If there are multiple devices associated with a Workspace, all these devices get the same authorization.

Inform your system administrator about the email address of your bot, so that they can set up the authorizations. They must repeat the following process for each workspace that has devices that your application is going to interact with:

1. From the customer view in [https://admin.webex.com](https://admin.webex.com), go to the *Workspaces* page. Search for the Workspace that contains the devices that you want to give the bot API access to. Click this Workspace to view the details.
2. In the Devices card, click *Edit API Access*. A list of all bots and users with authorization to access the API of the devices opens.
3. Click the plus sign (+) to add a new authorization. Choose the user or bot account that you want to authorize for the Workspace and select the appropriate access level. *Full Access* means that the user or bot can read device details, invoke commands and query status. *Read Only* means that the user or bot can only read device details and query status.

## Devices API

The [Devices API](https://developer.webex.com/docs/api/v1/devices) is the management API for the devices in your organization. You can use it to view some details on your devices, generate activation codes for adding new devices, or delete devices. In a device's details, you will find its *id*, which you will need to identify the device in any of the other APIs described in this guide.

### Finding the deviceId for a specific device

When calling any of the other device APIs, you always need to specify the `deviceId`.  The `deviceId` is generated when it a device is registered to the Cisco Webex cloud. It is good practice to avoid hardcoding the identifier.

Use the [GET List Devices method](https://developer.webex.com/docs/api/v1/devices/list-devices) to list devices: `GET https://webexapis.com/v1/devices/`

There are a lot of query parameters you can use to narrow down your search, see the [API reference](https://developer.webex.com/docs/api/v1/devices/list-devices) for details.

The command returns a list of devices that the authorized bot or user is entitled to see. There is one object for each device:

```json
{
    "items": [
        {
            "id": "...",
            ...
        },
        ...
    ]
}
```

Pay special attention to the following object fields:

- `id`: This is the `deviceId` that the bot or user must pass to any API call.
- `permissions`: The value of this field is an array. The bot or user can make xAPI calls only to the devices where "xapi" is part of this array. Always check the value of this field if you plan to use the xAPI, because the list of devices may also include devices that you are not permitted to make xAPI calls to.

## Device Configurations API

Once you know the `deviceId`, your application can perform a [GET /deviceConfigurations/](https://developer.webex.com/docs/api/v1/device-configurations/list-device-configurations-for-device) to read configurations for that device, or [PATCH /deviceConfigurations/](https://developer.webex.com/docs/api/v1/device-configurations/update-device-configurations) to change one or more of its configurations. The following sections explain the syntax to use when reading and writing configurations. You can find examples and try out the API in the [Device Configurations Reference](https://developer.webex.com/docs/api/v1/device-configurations) page.

### Syntax of a configuration

Each device configuration consists of the following properties:

```json
{
    "<configuration_key>": {
        "value": "", // Can be a string, number or boolean
        "source": "default",
        "sources": {
            "default": {
                "value": "" // Can be a string, number or boolean
                "editability": {
                    "editable": false, // Always false
                    "reason": "FACTORY_DEFAULT" // Always "FACTORY_DEFAULT"
                }
            },
            "configured": {
                "value": null // Can be null, a string, number or boolean
                "editability": {
                    "editable": false, // Can be true or false
                    "reason": "NOT_AUTHORIZED" // Can be "NOT_AUTHORIZED" or "CONFIG_MANAGED_BY_DIFFERENT_AUTHORITY"
                }
            }
        },
        "valueSpace": {}
    }
}
```

Each configuration has a unique path (`configuration_key`), which can be used to identify it in the API queries (more on this in the next section). At the root it has the value that is the effective `value` for the configuration that the device will observe, this is what will be used on the device. You don't directly control this effective value though, it is automatically calculated based on the `sources` below.

- `sources` is the collection of sources where configuration values come from. They may be a factory default or a configuration changed by an admin. Every source has a `value` for the configuration.
- `editability` shows editable if the source value can be changed through this API. If this source cannot be changed, reason will explain why that is.
- `source` shows which of the sources provides the effective `value` for the configuration.

The `default` source represents the factory default that the device has for the configuration. The `editable` for `editability` is always `false` since the device provides this source's `value`, and the `reason` for it not being editable is that the device provides this default: `"FACTORY_DEFAULT"`.

The `configured` source is where you can set a `value` through the API. If `value` here is not `null` the effective `value` for the configuration will automatically bet set to the `value` from `configured`, and the `source` for the configuration will be `"configured"`. If the `value` for `configured` is `null` the configuration `value` will come from the `default` in `sources` instead, and will have `source` set to `"default"`.

The configured source may not always be editable. The user calling the API may not be allowed to change any configurations due to their roles or scopes (`"NOT_AUTHORIZED"`) or that configuration may be managed elsewhere (`"CONFIG_MANAGED_BY_DIFFERENT_AUTHORITY"`), such as by a Cisco UCM.

The last part of a configuration is its `valueSpace`. This is defined by the device itself, and defines the requirements for a `value` for this configuration. The `default` field is the `value` when the source is `default`. Every value space has a `type` field.

Following are some examples of different types to illustrate how they work.

```json
{
  "Audio.DefaultVolume": {
      ...
      "valueSpace": {
        "default": 70,
        "maximum": 100,
        "minimum": 0,
        "type": "integer"
      }
  }
}
```

Any `value` for an `integer` type configuration cannot be lower than its `minimum` and cannot be higher than its `maximum`.

```json
{
  "Cameras.EncoderFaceDetection.Mode": {
    ...
    "valueSpace": {
      "default": "Off",
      "enum": ["Off", "On"],
      "type": "string"
    }
  }
}
```

Some `string` type configurations define an enum of possible values.

```json
{
  "NetworkServices.SMTP.Server": {
    "valueSpace": {
      "default": "",
      "maxLength": 255,
      "minLength": 0,
      "type": "string"
    }
  }
}
```

Other `string` type configurations allow any text to be entered as long as it satisfies the length requirements.

### Identifying a configuration

All configurations have a `configuration_key`, with which they can be identified. In the [PATCH API](https://developer.webex.com/docs/api/v1/device-configurations/update-device-configurations) (more on this later) they key is used to choose which configuration to modify, in the [GET API](https://developer.webex.com/docs/api/v1/device-configurations/list-device-configurations-for-device) it can be used to read one or multiple configurations. A `configuration_key` is composed of segments. Using the `key` query parameter, it's possible to filter configurations based on their keys in the following ways:

- **Absolute** is specifying a whole `configuration_key`, this gives at most one configuration as a result. `Conference.MaxReceiveCallRate` for example gives the `Conference MaxReceiveCallRate` configuration.
- **Wildcards** (*) is how you can search for multiple configurations that share segments. `Audio.Ultrasound.*` for example will return all configurations that start with `Audio Ultrasound`.
- **Range** ([*number*]) can be used to filter configurations with numbered segments. `FacilityService.Service` for instance has several numbered occurrences. Searching for `FacilityService.Service[1].Name` only shows the first `FacilityService Service Name` configuration, `FacilityService.Service[*].Name` shows all, `FacilityService.Service[1..3].Name` shows the first three and `FacilityService.Service[2..n].Name` shows all starting from 2.

### Updating configurations using JSON Patch

To make changes to configurations you can use the [Update Device Configurations API](https://developer.webex.com/docs/api/v1/device-configurations/update-device-configurations). You change a configuration by editing the `value` of its `configured` source. This API uses [JSON Patch](https://tools.ietf.org/html/rfc6902) syntax to make it possible to update multiple configurations in one request. In JSON Patch syntax, you send the API a list of operations, all of which are executed in the handling of the request. In the Device Configurations API you will only use the `replace` operation to set the configured `value` of a configuration, and `remove` operation to remove the configured `value` and revert to `default`. Below is an example PATCH that uses both operations to illustrate.

```json
[
  {
    "op": "replace",
    "path": "Audio.Ultrasound.MaxVolume/sources/configured/value",
    "value": 50
  },
  {
    "op": "remove",
    "path": "Conference.MaxReceiveCallRate/sources/configured/value"
  }
]
```

The `replace` operation will set `50` as the `value` in the `configured` source for the configuration `Audio.Ultrasound.MaxVolume`. The `remove` operation will remove the `value` in the `configured` source for `Conference.MaxReceiveCallRate` (if it was present), which will make that configuration use its `value` from the `default` source as its effective `value`.

When using JSON Patch you are **required** to specify a `Content-Type` header with value `application/json-patch+json`. 

### Example

Here, we first look up the device we want to modify, then read all configurations under Video Selfview, and then in one update request, we change all the settings we want to change.

#### Find device

We start with a GET request:
`https://webexapis.com/v1/devices?displayName=Harold&product=DX80`

The query parameters for filtering devices do not require the full search phrase to match, so searching for `Harold` will find both `Harold Smith` and `Harold Jones`. And searching for `DX80` will give you all `Cisco Webex DX80` devices despite not specifying the full product name.

Header fields:

```text
Authorization: Bearer <access token for the user>
Accept: application/json
```

The response has HTTP response code 200 and body:

```json
{
  "items": [
    {
      "id": "Y2lzY29zcGFyazovL3VybjpURUFNOnVzLWVhc3QtMl9hL0RFVklDRS8yMzc1NTEzZS1hMzEyLTQyY2ItOGY5Zi02MGFlZDAwNWYyYTY=",
      "displayName": "Harold Nordlund",
      "product": "Cisco Webex DX80",
      ...
    }
  ]
}
```

We can then take the `id` found in that response and use it to read all Video Selfview configurations for Harold's Webex DX80.

#### Read configurations

We do that with another GET request:
`https://webexapis.com/v1/deviceConfigurations?deviceId=Y2lzY29zcGFyazovL3VybjpURUFNOnVzLWVhc3QtMl9hL0RFVklDRS8yMzc1NTEzZS1hMzEyLTQyY2ItOGY5Zi02MGFlZDAwNWYyYTY&key=Video.Selfview.*`

We used a **wildcard** to read all configurations that start with the segments `Video.Selfview`.

Header fields:

```text
Authorization: Bearer <access token for the user>
Accept: application/json
```

The response has HTTP response code 200 and body:

```json
{
  "deviceId": "Y2lzY29zcGFyazovL3VybjpURUFNOnVzLWVhc3QtMl9hL0RFVklDRS8yMzc1NTEzZS1hMzEyLTQyY2ItOGY5Zi02MGFlZDAwNWYyYTY=",
  "items": {
    "Video.Selfview.OnCall.Duration": {
      "value": 15,
      "source": "configured",
      "sources": {
        "configured": {
          "value": 15,
          "editability": {
            "editable": true
          }
        },
        "default": {
          "value": 10,
          "editability": {
            "editable": false,
            "reason": "FACTORY_DEFAULT"
          }
        }
      },
      "valueSpace": {
        "type": "integer",
        "maximum": 60,
        "minimum": 1
      }
    },
    "Video.Selfview.Mirrored": {
      "value": "On",
      "source": "default",
      "sources": {
        "configured": {
          "value": null,
          "editability": {
            "editable": true
          }
        },
        "default": {
          "value": "On",
          "editability": {
            "editable": false,
            "reason": "FACTORY_DEFAULT"
          }
        }
      },
      "valueSpace": {
        "enum": [
          "Off",
          "On"
        ],
        "type": "string"
      }
    },
    "Video.Selfview.Default.PIPPosition": {
      "value": "LowerLeft",
      "source": "configured",
      "sources": {
        "configured": {
          "value": "LowerLeft",
          "editability": {
            "editable": true
          }
        },
        "default": {
          "value": "Current",
          "editability": {
            "editable": false,
            "reason": "FACTORY_DEFAULT"
          }
        }
      },
      "valueSpace": {
        "enum": [
          "CenterLeft",
          "CenterRight",
          "Current",
          "LowerLeft",
          "LowerRight",
          "UpperCenter",
          "UpperLeft",
          "UpperRight"
        ],
        "type": "string"
      }
    },
    ...
  }
}
```

We can see here that both `Video.Selfview.OnCall.Duration` and `Video.Selfview.Default.PIPPosition` have a configured value, while `Video.Selfview.Mirrored` has its default value as effective value. We'll do an update request to change these settings.

#### Change configurations

We do that with a PATCH request:
`https://webexapis.com/v1/deviceConfigurations?deviceId=Y2lzY29zcGFyazovL3VybjpURUFNOnVzLWVhc3QtMl9hL0RFVklDRS8yMzc1NTEzZS1hMzEyLTQyY2ItOGY5Zi02MGFlZDAwNWYyYTY`

Header fields:

```http
Authorization: Bearer <access token for the bot or user>
Content-Type: application/json-patch+json
Accept: application/json
```

Request body:

```json
[
  {
    "op": "replace",
    "path": "Video.Selfview.OnCall.Duration/sources/configured/value",
    "value": 50
  },
  {
    "op": "replace",
    "path": "Video.Selfview.Mirrored/sources/configured/value",
    "value": "Off"
  },
  {
    "op": "remove",
    "path": "Video.Selfview.Default.PIPPosition/sources/configured/value"
  }
]
```

Here we set a new value `50` for `Video.Selfview.OnCall.Duration`, we override the default for `Video.Selfview.Mirrored` with `"Off"`, and we revert to using the default value for `Video.Selfview.Default.PIPPosition`.

The response has HTTP response code 200 and body:

```json
{
  "deviceId": "Y2lzY29zcGFyazovL3VybjpURUFNOnVzLWVhc3QtMl9hL0RFVklDRS8yMzc1NTEzZS1hMzEyLTQyY2ItOGY5Zi02MGFlZDAwNWYyYTY=",
  "items": {
    "Video.Selfview.OnCall.Duration": {
      "value": 50,
      "source": "configured",
      "sources": {
        "configured": {
          "value": 50,
          "editability": {
            "editable": true
          }
        },
        "default": {
          "value": 10,
          "editability": {
            "editable": false,
            "reason": "FACTORY_DEFAULT"
          }
        }
      },
      "valueSpace": {
        "type": "integer",
        "maximum": 60,
        "minimum": 1
      }
    },
    "Video.Selfview.Mirrored": {
      "value": "Off",
      "source": "configured",
      "sources": {
        "configured": {
          "value": null,
          "editability": {
            "editable": true
          }
        },
        "default": {
          "value": "On",
          "editability": {
            "editable": false,
            "reason": "FACTORY_DEFAULT"
          }
        }
      },
      "valueSpace": {
        "enum": [
          "Off",
          "On"
        ],
        "type": "string"
      }
    },
    "Video.Selfview.Default.PIPPosition": {
      "value": "Current",
      "source": "default",
      "sources": {
        "configured": {
          "value": "LowerLeft",
          "editability": {
            "editable": true
          }
        },
        "default": {
          "value": "Current",
          "editability": {
            "editable": false,
            "reason": "FACTORY_DEFAULT"
          }
        }
      },
      "valueSpace": {
        "enum": [
          "CenterLeft",
          "CenterRight",
          "Current",
          "LowerLeft",
          "LowerRight",
          "UpperCenter",
          "UpperLeft",
          "UpperRight"
        ],
        "type": "string"
      }
    },
    ...
  }
}
```

The response here will contain all configurations for the device in question, including the ones that we changed in the PATCH request. You can verify in the response that our changes were applied.

## xAPI

Using the `deviceId`, your application can perform a [GET /xapi/status](https://developer.webex.com/docs/api/v1/xapi/query-status) to query the status, or [POST /xapi/command](https://developer.webex.com/docs/api/v1/xapi/execute-command) to invoke a command on that device.

For integrations that were authorized by an organization Administrator, the scopes that they authorized determine which types of commands the application may call. For bots, or integrations authorized by non-administrators, the access level of the bot or user determines if you have access to both commands and status, or only to status.

Read Only:

- Access to xStatus, which is an [HTTP GET request](https://developer.webex.com/docs/api/v1/xapi/query-status).

Full Access:

- Access to xStatus, which is an [HTTP GET request](https://developer.webex.com/docs/api/v1/xapi/query-status).
- Access to xCommand, which is an [HTTP POST request](https://developer.webex.com/docs/api/v1/xapi/execute-command).

The following sections explain the syntax to use when invoking a command or querying a status and how to translate from terminal mode to Webex REST API calls. You can find examples and try out the commands yourself in the [xAPI Reference](https://developer.webex.com/docs/api/v1/xapi) page.

### General recipe to invoke a command

The xAPI commands and statuses are described in the [Cisco Collaboration Endpoint Software API Reference Guide](https://www.cisco.com/c/en/us/support/collaboration-endpoints/spark-room-kit-series/products-command-reference-list.html). The guide uses [terminal mode notation](https://developer.webex.com/docs/device-developers-guide#device-configurations-and-xapi-reference-guide). All commands and statuses are not available for all types of devices. The guide states clearly which devices a command or status applies to.

To invoke a command on a device, use the following endpoint: `POST https://webexapis.com/v1/xapi/command/{commandKey}`

#### Command key

`commandKey` is the xCommand path.

- The command key is not case sensitive.
- The path segments are separated by dots (".").

#### Header

Include the following header fields:

```http
Authorization: Bearer <access token for the bot or user>
Content-Type: application/json
Accept: application/json
```

#### Command body

The command body is a JSON object. The object contains both the `deviceId` and an object with the arguments of the command. A command takes zero, one or more arguments.

```json
{
    "deviceId": "...",
    "arguments": {
        "argOne": "string",
        "argTwo": "literal",
        "argThree": integer value,
        "argFour": true or false,
        "argFive": [1, 2, 3]
    }
}
```

- Add all the command arguments in the `arguments` object in the body of the HTTP request.
- If the command doesn't have arguments, you can either omit the `arguments` object or insert an empty object.
- If the command has more than one argument, separate them by comma (",")
- If the command has multiple instances of the same argument, add the argument's value as an array (one array element for each instance).
- If the value is a string or a literal, put the value in quotes ("value"). Don’t use quotes for integer and boolean values.

#### Command response

A command response is a complex JSON object. This object contains the `deviceId`, an object with the arguments of the command (as explained in the previous section), and an object with the results of the command.

```json
{
    "deviceId": "...",
    "arguments": {
        ...
    }
    "result": {
        ...
    }
}
```

- The `result` object may contain arrays.
- An array always consists of complex objects with a key named `id`. This key is used to detect gaps in sparse arrays.
- If the command doesn't return any value, an empty `result` object is returned.

#### Example 1

This example shows how to translate a command from [terminal mode notation](https://developer.webex.com/docs/device-developers-guide#device-configurations-and-xapi-reference-guide) to the format you use for the Webex API.

Command in terminal mode: `xCommand Presentation Start Layout: Equal ConnectorId: 2 ConnectorId: 3 SendingMode: LocalRemote`
(For testing, use `ConnectorId: 1 ConnectorId: 2` instead if you have a DX70, DX80, SX20, Room Kit, or Room Kit Mini. These products don’t have a connector number 3.)

Since this is a **command** the REST API action is a POST: `https://webexapis.com/v1/xapi/command/Presentation.Start`

Header fields:

```http
Authorization: Bearer <access token for the bot or user>
Content-Type: application/json
Accept: application/json
```

Request body:

```json
{
    "deviceId": "...",
    "arguments": {
        "Layout": "Equal",
        "ConnectorId": [2, 3],
        "SendingMode": "LocalRemote"
    }
}
```

The expected return for this request is the HTTP response code 200, and the following response body:

```json
{
    "deviceId": "...",
    "arguments": {
        "Layout": "Equal",
        "ConnectorId": [
            2,
            3
        ],
        "SendingMode": "LocalRemote"
    },
    "result": {
        "Instance": 1
    }
}
```

#### Example 2

In this example we convert `xCommand Time DateTime Get` to the Webex API format. This command takes no arguments.

Since this is a **command** the REST API action is a POST: `https://webexapis.com/v1/xapi/command/Time.DateTime.Get`

Header fields:

```text
Authorization: Bearer <access token for the bot or user>
Content-Type: application/json
Accept: application/json
```

Request body:

```json
{
   "deviceId": "..."
}
```

The expected return for this request is the HTTP response code 200, and the following response body:

```json
{
    "deviceId": "...",
    "arguments": {},
    "result": {
        "Year": 2019,
        "Month": 5,
        "Day": 4,
        "Hour": 13,
        "Minute": 37,
        "Second": 0
    }
}
```

We recommend you to use the [xAPI Reference](https://developer.webex.com/docs/api/v1/xapi/execute-command) page to try more commands and see the response you receive.

### General recipe to query a status

To query a status on a device, send an HTTP GET request to the following endpoint: `https://webexapis.com/v1/xapi/status/?name={statusKey}&deviceId={deviceId}`

In contrast to commands, the `deviceId` is part of the URI of a status request, and a status request doesn't have a body.

#### Status key

`statusKey` is a list containing one or more xStatus paths.

- The status key is not case sensitive.
- The path segments are separated by dots (".").
- The status key may contain one or more wildcards. The wildcard will match all nodes that are deeper in the path hierarchy. The wildcard can represent any node, not only leaf nodes.
- When referring to elements in an array, you can choose to use one specific index, a specified range of indexes, or a wildcard (all indexes).

Here are some more status key examples with wildcards and arrays:

- `statusKey = Audio.*` - returns all the Audio status.
- `statusKey = *.Volume` - returns all Volume status nodes, irrespective of parent node.
- `statusKey = Audio.Input.Connectors.HDMI[1].Mute` - returns the mute status for one specific HDMI input connector.
- `statusKey = Audio.Input.Connectors.HDMI[2..3].Mute` - returns the mute status for a range of HDMI input connectors.
- `statusKey = Audio.Input.Connectors.HDMI[*].Mute` - returns the mute status for all HDMI input connectors.
- `statusKey = Audio.Input.Connectors.HDMI[*].*` - returns all the mute for all HDMI input connectors.

#### Header

Include the following header fields:

```text
Authorization: Bearer <access token for the bot or user>
Accept: application/json
```

#### Status response

A status response is a complex JSON object. The object contains the `deviceId` and an object with the results of the status query.

```json
{
    "deviceId": "...",
    "result": {
        ...
    }
}
```

- The `result` object may contain arrays.
- An array always consists of complex objects with a key named `id`. This key is used to detect gaps in sparse arrays.

#### Example 1

This example shows how to translate a status from [terminal mode notation](https://developer.webex.com/docs/device-developers-guide#device-configurations-and-xapi-reference-guide) to the format you use for the Webex API.

Status in terminal mode: `xStatus Audio Microphones Mute`

Since this is a **status request** the REST API action is a GET: `https://webexapis.com/v1/xapi/status/?name=Audio.Microphones.Mute&deviceId={deviceId}`

You must replace {deviceId} with the real deviceId.

Header fields:

```http
Authorization: Bearer <access token for the bot or user>
Accept: application/json
```

The expected return for this request is the HTTP response code 200, and the following response body:

```json
{
    "deviceId": "...",
    "result": {
        "Audio": {
            "Microphone": {
            "Mute": Off
            }
        }
    }
}
```

#### Example 2

In this example we retrieve both `xStatus Bookings Availability Status` and `xStatus RoomAnalytics RoomInUse` in a single call to the Webex API.

Since this is a status request the REST API action is a GET: `https://webexapis.com/v1/xapi/status/?name=Bookings.Availability.Status&name=RoomAnalytics.RoomInUse&deviceId={deviceId}`

You must replace {deviceId} with the real deviceId.

Header fields:

```http
Authorization: Bearer <access token for the bot or user>
Accept: application/json
```

The expected return for this request is the HTTP response code 200, and the following response body:

```json
{
    "deviceId": "...",
    "result": {
        "Bookings": {
            "Availability": {
                "Status": "Free"
            }
        },
        "RoomAnalytics": {
            "RoomInUse": "False"
        }
    }
}
```

We recommend that you use the [xAPI Reference](https://developer.webex.com/docs/api/v1/xapi/query-status) page to try more status queries and see the
 response you receive.

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

## Workspaces API

The [Workspaces API](https://developer.webex.com/docs/api/v1/workspaces) is the management API for the workspaces in your organization. You can use it to
 view and update details on your workspaces, to create new workspaces or to delete workspaces.

### Creating a workspace and adding a device

Using the [POST /workspaces](https://developer.webex.com/docs/api/v1/workspaces/create-a-workspace) endpoint, we can create a new workspace, populating the workspace `name`, `type` and `capacity` in the request payload. Additionally, there are optional fields supported in POST, such as `workspaceLocationId`, `floorId`, `calling`, `calendar`, `supportedDevices` and `notes`. The `workspaceLocationId` must be provided when the `floorId` is set. Only `freeCalling`, `webexEdgeForDevices`, `hybridCalling` and `webexCalling` calling types can be assigned via a POST request; the other calling types are configured via other mechanisms. If you do not choose a specific calling type, `freeCalling` will be your default. For calendar types, you can use `none`, `google` and `microsoft`. If you do not choose a specific calendar type, `none` will be set as the default. If you do not specify what devices are supported for the workspace, `collaborationDevices` will be set as the default. Give context to your workspaces with the `notes` field:

```json
{
    "displayName": "Conference Room",
    "workspaceLocationId":"YL34GrT...",
    "floorId":"Y2lzY29z...",
    "type": "meetingRoom",
    "capacity": 20,
    "calling": {
      "type": "webexCalling",
      "webexCalling":{
            "phoneNumber":"+12145652892",
            "extension":"64832",
            "locationId":"Y2lzY29..."
        }
     },
    "calendar": {
      "type": "microsoft",
      "emailAddress": "email@example.com"
    },
    "notes": "This is a note.",
    "supportedDevices": "phones"
}
```

A workspace `id` is automatically assigned each time a new workspace is created, and the response object will contain that `id`:

```json
{
    "id": "12345",
    "workspaceLocationId":"YL34GrT...",
    "floorId":"Y2lzY29z...",
    "displayName": "Conference Room",
    "type": "meetingRoom",
    "capacity": 20,
    "calling": {
      "type": "freeCalling"
    },
    "calendar": {
      "type": "microsoft",
      "emailAddress": "email@example.com"
    },
    "notes": "This is a note.",
    "supportedDevices": "phones"
}
```

Having created a new workspace, you can pass the `workspaceId` as `id` to the [Device Activation Code endpoint](https://developer.webex.com/docs/api/v1/devices/create-a-device-activation-code) (here called `placeId`) in order to generate a code that can be used to register a device to the workspace.

### Editing a workspace

You can update details for a workspace by specifying the `workspaceId` in the workspace `id` parameter in the URI.  Use the endpoint 
[PUT /workspaces](https://developer.webex.com/docs/api/v1/workspaces/update-a-workspace) to edit a workspace, populating all details that are present in a
[GET request for the workspace details](https://developer.webex.com/docs/api/v1/workspaces/get-workspace-details). Only `freeCalling`,  `hybridCalling` and  `webexCalling` calling types can be updated. The `locationId` field cannot be updated, but it must be present when updating the `webexCalling` phone number or extension fields.

Request:

```json
{
    "id": "12345",
    "displayName": "Conference Room",
    "workspaceLocationId":"YL34GrT...",
    "calling": {
      "type": "webexCalling",
      "webexCalling":{
            "phoneNumber":"+12145652892",
            "extension":"64832",
            "locationId":"Y2lzY29..."
        }
     },
    "floorId":"Y2lzY29z...",
    "type": "meetingRoom",
    "capacity": 10,
    "notes": "This is a new note."
}
```

If you don’t include the optional fields, they will be reset to their default values. The `workspaceLocationId`, `floorId`, 
`calendar` and `calling` fields do not change when omitted from the update request. The `workspaceLocationId` must be provided when 
the `floorId` is set.

Response:

```json
{
    "id": "12345",
    "workspaceLocationId":"YL34GrT...",
    "floorId":"Y2lzY29z...",
    "displayName": "Conference Room",
    "type": "meetingRoom",
    "capacity": 10,
    "calling": {
      "type": "freeCalling"
       },
    "calendar": {
      "type": "microsoft",
      "emailAddress": "email@example.com"
       },
    "notes": "This is a new note.",
    "supportedDevices": "phones"
}
```

## Workspace Locations API

The Workspace Locations API is the management API for the locations of your organization. A Workspace Location is a physical location with a name, address, country, city, latitude and longitude. Locations can have floors with a display name and a floor number.

### Creating a workspace location

Using the POST /workspaceLocations endpoint, we can create a new location, populating the location `displayName`, `address`, `countryCode` (ISO 3166-1), `latitude` and `longitude` in the request payload. Additionally, there are optional fields supported in POST, such as `cityName` and `notes`.

```json
{
    "displayName":"Cisco Barcelona",
    "address":"Carrer de Pere IV, Barcelona, Spain",
    "countryCode":"ES",
    "cityName":"Barcelona",
    "latitude":41.4066147,
    "longitude":2.2007173,
    "notes":"A note about the location"
}
```

A location `id` is automatically assigned each time a new location is created, and the response object will contain that `id`:

```json
{
    "id": "Y2lzY29z...",
    "displayName":"Cisco Barcelona",
    "address":"Carrer de Pere IV, Barcelona, Spain",
    "countryCode":"ES",
    "cityName":"Barcelona",
    "latitude":41.4066147,
    "longitude":2.2007173,
    "notes":"A note about the location"
}
```

### Editing a workspace location

You can update details for a location by specifying the `locationId` in the location `id` parameter in the URI.  Use the endpoint
 PUT /workspaceLocations/{locationId} to edit a location, populating all details that are present in a GET request for the location details.

Request:

```json
{
    "id":"Y2lzY29z...",
    "displayName":"Cisco Barcelona",
    "address":"Carrer de Pere IV, Barcelona, Spain",
    "countryCode":"ES",
    "cityName":"Barcelona",
    "latitude":41.4066147,
    "longitude":2.2007173,
    "notes":"A new note about the location"
}
```

If you don’t include the optional `cityName` and `notes` fields, they will be reset to their default values.

Response:

```json
{
    "id":"Y2lzY29z...",
    "displayName":"Cisco Barcelona",
    "address":"Carrer de Pere IV, Barcelona, Spain",
    "countryCode":"ES",
    "cityName":"Barcelona",
    "latitude":41.4066147,
    "longitude":2.2007173,
    "notes":"A new note about the location"
}
```

### Creating a workspace location floor

Using the POST /workspaceLocations/{locationId}/floors endpoint, we can create a new floor, populating the `floorNumber` field in the request payload. Additionally, there is an optional field `displayName` supported in POST. If you don’t define the optional `displayName` field, it will not be included in the floor object.

```json
{
    "floorNumber":1,
    "displayName":"My custom name"
}
```

A floor `id` is automatically assigned each time a new floor is created, and the response object will contain that `id`:

```json
{
    "id":"Y2lzY29z...",
    "locationId": "YL34GrT...",
    "floorNumber":1,
    "displayName":"My custom name"
}
```

### Editing a workspace location floor

You can update details for a floor by specifying the `floorId` in the floor `id` parameter in the URI.  Use the endpoint PUT /workspaceLocations/{locationId}/floors/{floorId} to edit a floor, populating all details that are present in a GET request for the floor details.

Request:

```json
{
    "floorNumber":2,
    "displayName":"My custom name"
}
```

If you don’t define the optional `displayName` field, it will not be included in the floor object.

Response:

```json
{
    "id":"Y2lzY29z...",
    "locationId": "YL34GrT...",
    "floorNumber":2,
    "displayName":"My custom name"
}
```
