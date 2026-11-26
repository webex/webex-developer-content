---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-calling-move-user-api-workflows
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Common Error Codes and Responses
- Response Format Examples
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webex-calling-move-user-api-workflows). [Full Markdown](../../../../docs/webex-calling-move-user-api-workflows.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Getting Started](002-getting-started.md)

## Article introduction

The [Webex Calling platform](https://developer.webex.com/docs/webex-calling-overview) provides comprehensive APIs for managing user configurations and locations. Among the most critical administrative operations is the ability to move users between locations while preserving their calling settings and minimizing service disruption. The Move User APIs enable administrators to automate complex user relocation scenarios that would otherwise require extensive manual configuration in [Webex Control Hub](https://www.webex.com/control-hub.html).

---

User moves in Webex Calling involve transferring users from one location to another within the same organization, along with their associated phone numbers and/or extensions, or assigning new ones as needed. For further details on features that are retained/removed during a move, see the `Features` section in [Move Calling users](https://help.webex.com/en-us/article/h68cdcb/Move-users-from-one-location-to-another#wbxch_t_move_user) help document.

## Parent context

## Common Error Codes and Responses

The Move User APIs return specific error codes to help identify and resolve issues during validation and execution. Understanding these error codes is essential for proper error handling and troubleshooting.

## Selected section

### Response Format Examples

<a id="error-response"></a>

#### Error Response

Error responses follow a consistent format with detailed error information:

```json
{
    "errors": [
        {
            "code": 1026016,
            "message": "User should have either phone number or extension."
        }
    ]
}
```

<a id="internal-server-error-response"></a>

#### Internal Server Error Response

For internal server errors, the response will be of the format:

```json
{
    "message": "The request could not be understood by the server due to malformed syntax.",
    "errors": [
        {
            "description": "The request could not be understood by the server due to malformed syntax."
        }
    ]
}
```
<a id="validation-response"></a>

#### Validation Response
Validation results with information on possible impacts and errors if any:
```json
{
    "response": {
        "usersList": [
            {
                "userId": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS85YzJhMDUxMC0wOTUwLTQ1MmYtODFmZi05YTVkMjM2OTJkZTY",
                "impacts": [
                    {
                        "code": 19701,
                        "message": "[Informational 19701] The identity/device profile the user is using is moved to the new group: GBKAXBRMJUXF, GNXX95CLTQ0V, HD_92dbc8b6-30d1-419f-9386-3340da658f9c, G4O4NVP7MZI5, GQGWO5BDMPLP."
                    },
                    {
                        "code": 19722,
                        "message": "[Informational 19722] User CLID number is set to use the new group CLID number: null."
                    },
                    {
                        "code": 19723,
                        "message": "[Informational 19723] New group CLID number is not configured."
                    }
                ],
                "errors": [
                    {
                        "code": 4202,
                        "message": "[Error 4202] The extension is not available. It is already assigned to a user: 7593. "
                    }
                ]
            }
        ]
    }
}
```

<a id="job-response"></a>

#### Job Response
Successful job creation returns detailed job information:

```json
{
    "response": {
        "jobDetails": {
            "name": "moveusers",
            "id": "Y2lzY29zcGFyazovL3VzL0pPQl9JRC9mZjBlN2Q2Ni05MDRlLTRkZGItYjJlNS05ZGM0ODk0ZDY5OTk",
            "trackingId": "ROUTER_ebb52b5b-d060-4164-9757-48b383423d73",
            "sourceUserId": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS85YzJhMDUxMC0wOTUwLTQ1MmYtODFmZi05YTVkMjM2OTJkZTY",
            "sourceCustomerId": "Y2lzY29zcGFyazovL3VzL09SR0FOSVpBVElPTi8wMjEyNGVlZi04YWY3LTQ4OWMtODA1Yi0zNjNjYzY0MDE4OTM",
            "targetCustomerId": "Y2lzY29zcGFyazovL3VzL09SR0FOSVpBVElPTi8wMjEyNGVlZi04YWY3LTQ4OWMtODA1Yi0zNjNjYzY0MDE4OTM",
            "instanceId": 10,
            "jobExecutionStatus": [
                {
                    "id": 10,
                    "startTime": "2023-06-08T12:05:11.798Z",
                    "lastUpdated": "2023-06-08T12:05:11.798Z",
                    "statusMessage": "STARTED",
                    "exitCode": "UNKNOWN",
                    "createdTime": "2023-06-08T12:05:11.752Z",
                    "timeElapsed": "PT0S"
                }
            ],
            "latestExecutionStatus": "STARTED",
            "latestExecutionExitCode": "UNKNOWN",
            "counts": {
                "totalMoves": 0,
                "moved": 0,
                "failed": 0,
                "pending": 0,
                "skipped": 0
            }
        }
    }
}
```
