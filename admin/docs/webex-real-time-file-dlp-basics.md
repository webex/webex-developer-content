---
type: Guide
title: Webex Real-time File DLP Basics | Consolidated Guide
display_title: Real-time File DLP Basics
canonical_url: https://developer.webex.com/docs/webex-real-time-file-dlp-basics
content_type: documentation
product_group:
- webex-suite
categories:
- admin
- compliance
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/webex-real-time-file-dlp-basics)

Webex provides a rich set of admin and compliance APIs to help Compliance Officers monitor and assert adherence to corporate policies, as they relate to information exchange and sharing. In this article we introduce the proactive, real-time, file Data Loss Prevention (DLP) compliance mechanism as the preferred way to control proliferation of files in a protected org.

## Roles and Licensing Requirements

The officer responsible for adherence to the corporate policies is called a Compliance Officer, which is a designated role in Control Hub. Notably this role is separate and distinct from that of an admin. The admin role is primarily concerned with the management of the system (user management, device management etc.), while the Compliance Officer role is primarily concerned with the management of content. All compliance APIs check for Compliance Officer scopes before allowing an API request.

In this article we will use the terms Compliance Officer and DLP/CASB (Cloud Access Security Broker) system somewhat synonymously. The CASB/DLP system is a software security framework with preprogrammed and configurable policies which ensures an enterprise adheres to corporate and legal policies. The DLP system uses the Compliance Officer role to interact with the Webex APIs ensuring that these rules and policies are enforced.



> **Info**
>
> The Control Hub GUI allows you to enable real-time file DLP, but you need to either integrate to it according to this article or use a DLP provider that already supports it. If you just turn it on without a functional framework, all file uploads from protected users will incur an additional latency as the default timer expires.





> **Warning**
>
> Org level messages webhooks trigger **only** when real-time file scanning (DLP) is enabled and **only** for messages that contain files.



![Webex Control Hub](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt6a4f9d08ae950083/61683e6d5547844ca4abf9b4/control-hub.png)

For a list of Webex compliance and archival partners see [here](https://help.webex.com/en-US/article/nmbm0jk/Webex-Integration-with-Archiving-and-Data-Loss-Prevention-Solutions).

### Licensing

Real-time file DLP needs an enterprise Webex account with the [ProPack license](https://help.webex.com/en-US/article/np3c1rm/Pro-Pack-For-Cisco-Webex-Control-Hub) purchased and applied.

## Advantages of Real-time File DLP

The real-time file DLP framework eliminates the polling of the events API for file events (other events like membership and message events still need to be queried from the events API). By its very nature this polling introduces latencies between when a file is accessible in a space until it will be remediated when policy violations mandate such actions. While often only on the order of 1 min, enterprises deemed this latency as too long, as it gave space members an opportunity to inspect, if not download a file.

The advantage of the real-time file DLP API is that a file can be accessed by other space members only after the file has been inspected and approved by the DLP system.

## User Experience

As it relates to the basic user experience of real-time file DLP there are 3 distinct outcomes. A DLP approved file, a default approved file, and a rejected file. Keep in mind that different clients may look slightly different and combining malware scanning with real-time file DLP may also result in slightly different messages.

### DLP Approved File

![DLP Approved File](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt2f31a2be1c78bf84/61683e6c19bdec3c9fc22761/download-screenshot.png)

The DLP `approved` file is not different in any way from today’s user experience. The user is not aware any file scanning has occurred.

### Default Approved File

There is a built-in timer of 10 seconds which will `approve` the file if the DLP system does not respond in time.

![Default Approved File](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blta9e1adc3dcd0ee27/61683e6d55bcc83601f7cfee/file-not-scanned.png)

There is an indication to the user that the file was not scanned for sensitive information.

### DLP Rejected File

The following shows the user experience for a file that was `rejected` by the DLP vendor typically due to some policy violation (leaking credit card numbers, PII data etc.).

![DLP Rejected File](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt653c87880ebd2866/61683e6cf748fa3c9d0236fe/blocked-file.png)

## Basic Flow for Real-time File DLP

The real-time file DLP mechanism diverts the flow at which the DLP system is invoked, compared to the current mechanism of event polling. That is, first the DLP system must approve the file, then it will be accessible to other participants. To achieve this flow, without impacting users with too much latency, we are introducing org-wide webhooks for Compliance Officers. An org wide webhook will be sent to the DLP system whenever a protected org user uploads a file. When the DLP system receives the webhook it will extract the content URL of the file in question which it will download via the Compliance Officer role. After inspection, the Compliance system will call either an `approve` on the file content, which will make it accessible to other space members, or a `reject`, which will mark the file as a violation in the space.
While the DLP system scans the file, the users in the space will see a busy indicator until a decision has been made. A default timeout of 10s approves the file in case the DLP system does not respond in time.



> **Info**
>
> Note: The real-time file DLP’s emphasis is on users of a protected organization to not upload and share `sensitive` information to a space. This is different from the also available [Malware protection](https://help.webex.com/en-US/article/yr6g4bb/Anti-Malware-Scanning-of-Files-in-Webex), in which protected users are protected from downloading corrupted files.



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

## Summary

Real-time file DLP provides a new, proactive way to inspect artifacts, before they can be accessed by other collaborators. Users uploading the file as well as space members are in the know if a file is compromised and the uploading user can redact the file content in question and try another upload.

Our real-time file DLP mechanism is the first in a row of many such real-time mitigation capabilities in Webex.
