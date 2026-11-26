---
type: Excerpt
canonical_url: https://developer.webex.com/docs/device-developers-guide
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- xAPI
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/device-developers-guide). [Full Markdown](../../../../docs/device-developers-guide.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Provision, manage and control your Webex devices.

---

An integrator can use the device APIs to integrate with devices. There are four APIs that can be used to interact with devices:

- **[Devices API](https://developer.webex.com/docs/devices#devices-api)**: The inventory of your devices that can be used to view and delete devices or to create activation codes for getting new devices online.
- **[Device Configurations API](https://developer.webex.com/docs/devices#device-configurations-api)**: View and update the configurations of any device, online or offline.
- **[Workspaces API](https://developer.webex.com/docs/devices#workspaces-api)**: Create, view, update and delete workspaces. Workspaces represent where people work, such as conference rooms and meeting spaces
- **[xAPI](https://developer.webex.com/docs/devices#xapi)**: Allows developers to programmatically invoke commands and query the status of devices.

## Selected section

## xAPI

Using the `deviceId`, your application can perform a [GET /xapi/status](https://developer.webex.com/docs/api/v1/xapi/query-status) to query the status, [POST /xapi/command](https://developer.webex.com/docs/api/v1/xapi/execute-command) to invoke a command, or [GET /xapi/schema](https://developer.webex.com/docs/api/v1/xapi/query-schema) to query the command and status schemas for that device.

For integrations that were authorized by an organization Administrator, the scopes that they authorized determine which xAPI operations the application may call. For bots, or integrations authorized by non-administrators, the access level of the bot or user determines if you have Full Access to commands, status, command schemas, and status schemas, or Read Only access to status and status schemas.

Read Only:

- Access to xStatus, which is an [HTTP GET request](https://developer.webex.com/docs/api/v1/xapi/query-status).
- Access to status schemas, which is an [HTTP GET request](https://developer.webex.com/docs/api/v1/xapi/query-schema).

Full Access:

- Access to xStatus, which is an [HTTP GET request](https://developer.webex.com/docs/api/v1/xapi/query-status).
- Access to xCommand, which is an [HTTP POST request](https://developer.webex.com/docs/api/v1/xapi/execute-command).
- Access to command and status schemas, which is an [HTTP GET request](https://developer.webex.com/docs/api/v1/xapi/query-schema).

The following sections explain the syntax to use when invoking a command, querying a status, or querying schemas, and how to translate from terminal mode to Webex REST API calls. You can find examples and try out the commands yourself in the [xAPI Reference](https://developer.webex.com/docs/api/v1/xapi) page.

### General recipe to invoke a command

The xAPI commands and statuses are described in the [Cisco Collaboration Endpoint Software API Reference Guide](https://www.cisco.com/c/en/us/support/collaboration-endpoints/spark-room-kit-series/products-command-reference-list.html). The guide uses [terminal mode notation](https://developer.webex.com/docs/device-developers-guide#device-configurations-and-xapi-reference-guide). All commands and statuses are not available for all types of devices. The guide states clearly which devices a command or status applies to.

To invoke a command on a device, use the following endpoint: `POST https://webexapis.com/v1/xapi/command/{commandKey}`

#### Command key

`commandKey` is the xCommand path.

- The command key is not case sensitive.
- The path segments are separated by dots (".").

#### Command request header

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

#### Command example 1

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

#### Command example 2

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

We recommend using the [xAPI Reference](https://developer.webex.com/docs/api/v1/xapi/execute-command) page to try more commands and see the response you receive.

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

#### Status request header

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

#### Status example 1

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

#### Status example 2

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

We recommend using the [xAPI Reference](https://developer.webex.com/docs/api/v1/xapi/query-status) page to try more status queries and see the response you receive.

### General recipe to query schemas

To query the JSON schemas for supported statuses and commands, send an HTTP GET request to the following endpoint: `https://webexapis.com/v1/xapi/schema?deviceId={deviceId}`

You must include at least one `deviceId`. A request can include up to five devices by repeating the query parameter: `?deviceId={deviceId}&deviceId={deviceId}`

By default, the response includes both status and command schemas if your access token has both xAPI scopes. You can limit the response with `status` and `command` query parameters:

- `status` filters status schemas by xStatus path expression and requires the `spark:xapi_statuses` scope.
- `command` filters command schemas by xCommand path expression and requires the `spark:xapi_commands` scope.
- You can repeat either filter to query multiple expressions in one request: `?deviceId={deviceId}&status=Foo.*&status=Bar.*&command=Bin.Baz`
- If you specify only `status` filters, the response includes only status schemas. If you specify only `command` filters, the response includes only command schemas.

#### Schema request header

Include the following header fields:

```text
Authorization: Bearer <access token for the bot or user>
Accept: application/json
```

#### Schema response

A schema response is an array with one object for each device. Each object contains the `deviceId` and the matching schemas.

```json
[
    {
        "deviceId": "...",
        "status": {
            "Conference.HideNonVideo.Active": {
                "schema": {
                    "enum": ["True", "False"],
                    "type": "string"
                }
            }
        },
        "commands": {
            "UserInterface.Extensions.Icon.Upload": {
                "arguments": {
                    "Id": {
                        "required": false,
                        "schema": {
                            "type": "string",
                            "maxLength": 128,
                            "minLength": 0
                        }
                    }
                },
                "resultSchema": {
                    "type": ["object", "null"]
                }
            }
        }
    }
]
```

We recommend using the [xAPI Reference](https://developer.webex.com/docs/api/v1/xapi/query-schema) page to try more schema queries and see the response you receive.
