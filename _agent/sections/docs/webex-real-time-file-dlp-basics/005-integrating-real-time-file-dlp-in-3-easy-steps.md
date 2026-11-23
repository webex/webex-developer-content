---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-real-time-file-dlp-basics
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Integrating Real-time File DLP in 3 Easy Steps
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webex-real-time-file-dlp-basics). [Full Markdown](../../../../docs/webex-real-time-file-dlp-basics.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Roles and Licensing Requirements](001-roles-and-licensing-requirements.md)

## Article introduction

Webex provides a rich set of admin and compliance APIs to help Compliance Officers monitor and assert adherence to corporate policies, as they relate to information exchange and sharing. In this article we introduce the proactive, real-time, file Data Loss Prevention (DLP) compliance mechanism as the preferred way to control proliferation of files in a protected org.

## Selected section

## Integrating Real-time File DLP in 3 Easy Steps

1. One time only: as a compliance officer, register an org-wide webhook to receive file upload notifications from protected users in your org.
1. Receive webhook notifications, extract the download URL and, as a Compliance Officer, download the file for inspection.
1. After the file scanning is complete, as a Compliance Officer, approve the file to make it accessible to all space members or reject the file to block it.

### Org-wide Webhook

Org wide webhooks are introduced in the [Webhook Guide](https://developer.webex.com/docs/webhooks) as admin webhooks. Here, for compliance use cases, the role needed is that of a compliance officer. The org-wide file upload events come in the form of message created events with a file attachment, similar to how they show in the /events API today.

A sample curl command to register an org-wide file upload webhook looks like

```bash
curl -X POST \
-H "Authorization: Bearer ${CO_TOKEN}" \
-H "Content-type: application/json" \
https://webexapis.com/v1/webhooks \
-d ‘{"name":"org_wide_file_webhook", "resource":"messages", "event":"created", "targetUrl":"https://www.sampletarget.com/webhookin/", \
"secret":"my#deep#secret!" \
"ownedBy":"org"}’
```

If you are using the Webex APIs for any interactive use case, this will all be very familiar to you. The only addition in the payload is that new field `"ownedBy":"org"`. There can only be 1 org wide webhook per resources, event and `appid` (Integration) in all of the org. As for any webhooks from Webex your targetUrl must be publicly accessible over the internet. If you are concerned about the validity of the webhook please check *webhook secrets* in the docs. Your CASB/DLP system will receive these notifications and act on them.

### Download and Scan the File

A sample webhook received for a file event looks like this:

```json
{
  "id": "Y2lzY29zcGFyazovL3VybjpURUFNOnVzLXdlc3QtMl9yL1dFQkhPT0svNjc5YWUzZjItOWU3Yy00NWU3LTlmZWQtOTNlODE2ZTVhNmQx",
  "name": "messages_created",
  "targetUrl": "http://api.webhookinbox.com/i/RkHN6Pg1/in/",
  "resource": "messages",
  "event": "created",
  "orgId": "Y2lzY29zcGFyazovL3VzL09SR0FOSVpBVElPTi83M2YwYmFlYS0yY2QxLTQwOWQtOTBkNi00MTMyYzcwYzc4NjE",
  "createdBy": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS8xNTM1MGQ0Zi0zOWE4LTRlYmUtYjVhOC1iOWRiNTZmMmQ1ZDg",
  "appId": "Y2lzY29zcGFyazovL3VzL0FQUExJQ0FUSU9OL0NmMzkyNWU5NDFmMzhhYTc0M2Y0MmFiNzcwZmZhZjFhNTIyMjcxZDI5OTQ4NDhjNjk2YWMwYTEwN2Q2YTg5MjI3",
  "ownedBy": "org",
  "status": "active",
  "created": "2021-10-12T21:39:51.253Z",
  "actorId": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS9iYmVjMGRmMC0wOWY0LTQ1YTYtODZkZS1mMTJlZDI1ZGEwYTM",
  "data": {
    "id": "Y2lzY29zcGFyazovL3VybjpURUFNOnVzLXdlc3QtMl9yL01FU1NBR0UvNWI1NzAyZjAtMmJhNS0xMWVjLWIyYWUtNmQwNjAwMzBkYTg2",
    "roomId": "Y2lzY29zcGFyazovL3VybjpURUFNOnVzLXdlc3QtMl9yL1JPT00vMmIwYTc2MDAtZmJjZi0xMWViLTg1NTItMDliODZiNzEwYTdh",
    "roomType": "group",
    "files": ["https://webexapis.com/v1/contents/Y2lzY29zcGFyazovL3VybjpURUFNOnVzLXdlc3QtMl9yL0NPTlRFTlQvNWI1NzAyZjAtMmJhNS0xMWVjLWIyYWUtNmQwNjAwMzBkYTg2LzA?allow=dlpEvaluating"],
    "personId": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS9iYmVjMGRmMC0wOWY0LTQ1YTYtODZkZS1mMTJlZDI1ZGEwYTM",
    "personEmail": "realtimeuser3@schiffert.me",
    "created": "2021-10-12T21:42:54.367Z"
  }
}
```

In the data section, note the `files` array with the content URL and the tail `allow=dlpEvaluating`. Only org wide files webhooks for orgs with the real-time file DLP enabled have this indicator, which is one of the files states asking the DLP system to evaluate/scan the file.

The following command will download the file to get it ready for inspection:

```bash
curl -X GET -H "Authorization: Bearer ${CO_TOKEN}" \ https://webexapis.com/v1/contents/Y2lzY29zcGFyazovL3VybjpURUFNOnVzLXdlc3QtMl9yL0NPTlRFTlQvNWI1NzAyZjAtMmJhNS0xMWVjLWIyYWUtNmQwNjAwMzBkYTg2LzA?allow=dlpEvaluating,dlpUnchecked
```

Appending the `dlpUnchecked` state will help force download files. These are file quarantine states that serve as filters. Other quarantine states include

* `dlpEvaluating`
* `dlpUnchecked`
* `dlpRejected`
* `dlpRejectedByDefault`



> **Info**
>
> Note: There is a 10 second default timeout for the CASB system to respond to the file upload after the webhook is sent. If the CASB system finds the file to be policy violating after the file has been approved under the default policy the CASB system must use the Compliance Officers privilege to DELETE any message. There is no way to change the final file states approved/rejected as it would cause user confusion in the GUI.



### Approve or Reject the File

To approve or reject files, make the following calls as Compliance Officer.

#### Approve

The following curl command will approve a file that has been cleared by the compliance system for distribution:

```bash
curl -X PUT \
-H "Authorization: Bearer ${CO_TOKEN}" \
-H "Content-type": application/json" \
https://webexapis.com/v1/contents/Y2lzY29zcGFyazovL3VybjpURUFNOnVzLXdlc3QtMl9yL0NPTlRFTlQvNWI1NzAyZjAtMmJhNS0xMWVjLWIyYWUtNmQwNjAwMzBkYTg2LzA?result=approve
```

### Reject

Conversely the following command will block a file from being distributed. A GUI bricklet indicates the file has been upload to all space users but the file cannot be accessed/downloaded and file previews are not rendered:

```bash
curl -X PUT \
-H "Authorization: Bearer ${CO_TOKEN}" \
-H "Content-type": application/json" \
https://webexapis.com/v1/contents/Y2lzY29zcGFyazovL3VybjpURUFNOnVzLXdlc3QtMl9yL0NPTlRFTlQvNWI1NzAyZjAtMmJhNS0xMWVjLWIyYWUtNmQwNjAwMzBkYTg2LzA?result=reject
```

If the file quarantine state has been changed to a final `approve` or `reject` (usually under the default timeout) and the Compliance Officer tries to change the file quarantine state, an error message similar to the following will be returned: 

```json
{
    "message": "File Status has been changed and can not be updated anymore.",
    "errors": [
        { "description": "File Status has been changed and can not be updated anymore." }
    ],
    "trackingId": "ROUTER_616608A2-CC10-01BB-04E6-806BF1BA04E6"
}
```
