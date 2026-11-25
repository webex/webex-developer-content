---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-calling-move-user-api-workflows
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Common Error Codes and Responses
- Request Format Examples
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

### Request Format Examples

<a id="single-user-validation-request"></a>

#### Single User Validation Request

```json
{
  "usersList": [
    {
      "locationId": "Y2lzY29zcGFyazovL3VzL0xPQ0FUSU9OLzMxMTkwZjQtZjBiOS00",
      "validate": true,
      "users": [
        {
          "userId": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS8xZTJjNzBlZC00ZDYtNGYyYy05",
          "extension": "1001",
          "phoneNumber": "+18632520486"
        }
      ]
    }
  ]
}
```

<a id="single-user-move-request"></a>

#### Single User Move Request

```json
{
  "usersList": [
    {
      "locationId": "Y2lzY29zcGFyazovL3VzL0xPQ0FUSU9OLzMxMTkwZjQtZjBiOS00",
      "validate": false,
      "users": [
        {
          "userId": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS8xZTJjNzBlZC00ZDYtNGYyYy05",
          "extension": "1001",
          "phoneNumber": "+18632520486"
        }
      ]
    }
  ]
}
```

<a id="bulk-user-move-request"></a>

#### Bulk User Move Request

```json
{
    "usersList": [
        {
            "locationId": "Y2lzY29zcGFyazovL3VzL0xPQ0FUSU9OLzVmMDI3OGZlLWU4OGMtNDMzNy04MGViLWRjY2NiM2VlMDU1MA",
            "validate": false,
            "users": [
                {
                    "userId": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS9teW5hbWUgaXNvcHRpdXMGEyltZXdlYXJlMGEyMGEyNWM1OWE",
                    "phoneNumber": "+18632520486"
                },
                {
                    "userId": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS8wNTJhYjliZC1jNmUyLTZlYWUtMWE5YS01ZWZhMGEyNWMxNmE",
                    "extension": "28544"
                }
            ]
        },
        {
            "locationId": "Y2lzY29zcGFyazovL3VzL0xPQ0FUSU9OLzVmMDI3OGZlLWU4OGMtNDkwNS04MGViLWRjY2NiM2VlMTQ0MwFG",
            "validate": false,
            "users": [
                {
                    "userId": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS85YzJhMDUxMC0wOTUwLTQ1MmYtODFmZi05YTVkMjM2OTJkZTY",
                    "extension": "29376",
                    "phoneNumber": "+18947028597"
                }
            ]
        }
    ]
}
```
