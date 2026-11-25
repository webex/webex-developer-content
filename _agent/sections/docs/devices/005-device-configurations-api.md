---
type: Excerpt
canonical_url: https://developer.webex.com/docs/devices
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Device Configurations API
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
