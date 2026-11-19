---
type: Guide
title: Access Meeting Resources Guide | Consolidated Guide
display_title: Meeting Resource Guide
canonical_url: https://developer.webex.com/docs/access-meeting-resources-guide
content_type: documentation
product_group:
- webex-suite
categories:
- meeting
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/access-meeting-resources-guide)

Use this guide to learn how to code to access the meeting resources from Webex.

## Access Meeting Resources Guide
Sales enablement needs to know what meetings are occurring, who the participants in each individual meeting, when these meetings start and end and how to access the content from these meetings. Web developers have asked for improved availability of connecting to the resources that allow applications to be meeting aware and get access to post meeting resources.

### Getting Started
To leverage assets from a meeting, you must first ensure the following settings are enabled in Webex when the meeting starts:

* Recording: To record the meeting, you must enable the recordings option.  This can be done by the users during a meeting or programmatically via API for a scheduled meeting.

*	Transcripts: To create a transcript, you must turn on Webex Assistant. This cannot be done programmatically and must be turned on by the meeting host/participant or set as default behavior in the control hub. NOTE: Webex Assistant requires a license.

### Accessing Meeting Resources
When a meeting ends, Webex triggers a notice that unlock any meeting assets and you may retrieve them.

To achieve this via APIs, you must create a webhook for the meeting termination.

The documentation for the Webhook APIs can be found at https://developer.webex.com/docs/api/v1/webhooks/create-a-webhook

Creation is a post request to /v1/webhooks event = ended and resource = meetings

The post might look like below:
```javascript
{
  "name": "Meeting Ended Webhook",
  "targetUrl": "https://example.com/mywebhook",
  "resource": "meetings",
  "event": "ended",
}

```
Then the response might be something like:

```javascript
{
    "id": "Y2lzY29zcGFyazovL3VybjpURUFNOnVzLXdlc3QtMl9yL1dFQkhPT0svNDk5ZjkxZjItY2QxMi00NTk2LWEzYjctNDY4NTA1OGQ2NTlm",
    "name": "Meeting Ended Webhook",
    "targetUrl": "https://webhook.site/c231a24c-8a04-42b6-a7ed-85ff1a51b60b",
    "resource": "meetings",
    "event": "ended",
    "orgId": "Y2lzY29zcGFyazovL3VzL09SR0FOSVpBVElPTi81NWM1YWUzZi04ZDdmLTQyN2ItYTRmOS01ZTNjYjNkZGRmN2I",
    "createdBy": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS9hYzAxZjUzMi1kMDIyLTRmOGUtYTQ5NC1mMGE0ZDc5ZTUyMjc",
    "appId": "Y2lzY29zcGFyazovL3VzL0FQUExJQ0FUSU9OL0NmMzkyNWU5NDFmMzhhYTc0M2Y0MmFiNzcwZmZhZjFhNTIyMjcxZDI5OTQ4NDhjNjk2YWMwYTEwN2Q2YTg5MjI3",
    "ownedBy": "creator",
    "status": "active",
    "created": "2021-05-14T20:20:01.024Z"
}
```

If you want to synchronize your app with all meetings, there are webhooks for the following categories: created, updated, and deleted.

The webhook you receive for a meeting end might look something like:

```javascript
{
  "id": "Y2lzY29zcGFyazovL3VybjpURUFNOnVzLXdlc3QtMl9yL1dFQkhPT0svNDk5ZjkxZjItY2QxMi00NTk2LWEzYjctNDY4NTA1OGQ2NTlm",
  "name": "Meeting Ended Webhook",
  "targetUrl": "https://webhook.site/c231a24c-8a04-42b6-a7ed-85ff1a51b60b",
  "resource": "meetings",
  "event": "ended",
  "orgId": "Y2lzY29zcGFyazovL3VzL09SR0FOSVpBVElPTi81NWM1YWUzZi04ZDdmLTQyN2ItYTRmOS01ZTNjYjNkZGRmN2I",
  "createdBy": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS9hYzAxZjUzMi1kMDIyLTRmOGUtYTQ5NC1mMGE0ZDc5ZTUyMjc",
  "appId": "Y2lzY29zcGFyazovL3VzL0FQUExJQ0FUSU9OL0NmMzkyNWU5NDFmMzhhYTc0M2Y0MmFiNzcwZmZhZjFhNTIyMjcxZDI5OTQ4NDhjNjk2YWMwYTEwN2Q2YTg5MjI3",
  "ownedBy": "creator",
  "status": "active",
  "created": "2021-05-14T20:20:01.024Z",
  "data": {
    "id": "501e995485e2460bb129410116757b13_I_194316955237236650",
    "meetingType": "meeting",
    "timezone": "UTC",
    "start": "2021-05-14T20:25:19Z",
    "end": "2021-05-14T20:26:54Z",
    "hostUserId": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS9hYzAxZjUzMi1kMDIyLTRmOGUtYTQ5NC1mMGE0ZDc5ZTUyMjc",
    "state": "ended",
    "hostEmail": "spouliottes@gmail.com",
    "siteUrl": "spouliottes-test.webex.com",
    "orgId": "55c5ae3f-8d7f-427b-a4f9-5e3cb3dddf7b"
  }
}
```
It is important to remember that you need to store the ID in the data.  Webex supports listing meetings but they only return future and in progress meetings. You cannot recover this IS historically and need to store in your app.

Developer Note: When a meeting is created, the ID will look different than post meeting ID in webhook. Webex appends an additional ID that is demarcated with
“_I_”. For example, in the above case the ID on end event was: '501e995485e2460bb129410116757b13_I_194316955237236650'

In the pre-meeting creation, the ID for the event would have been: '501e995485e2460bb129410116757b13'

### Find Recording Assets
After a meeting has finished, Webex will process and store post meeting assets and make them available through the endpoint: -	/v1/recordings

You can query for all available recordings by leaving the query parameters blank or you can set specific data such as meetingId as in the example below: https://webexapis.com/v1/recordings?meetingId=501e995485e2460bb129410116757b13_I_194316955237236650

The response will look something like this:
```javascript
{
  "items": [
    {
      "id": "724a81a697201039a976005056819cde",
      "meetingId": "501e995485e2460bb129410116757b13_I_194316955237236650",
      "scheduledMeetingId": "501e995485e2460bb129410116757b13_20210514T203000Z",
      "meetingSeriesId": "501e995485e2460bb129410116757b13",
      "topic": "Test meeting-20210514 2025-1",
      "createTime": "2021-05-14T20:28:53Z",
      "siteUrl": "spouliottes-test.webex.com",
      "downloadUrl": "https://spouliottes-test.webex.com/spouliottes-test/lsr.php?RCID=77ab059a6b6512550d6a3ddafeea57aa",
      "playbackUrl": "https://spouliottes-test.webex.com/spouliottes-test/ldr.php?RCID=6197666928e747419d239f3cfdee3e49",
      "password": "tA3hwXUm",
      "format": "MP4",
      "durationSeconds": 85,
      "sizeBytes": 4982263,
      "shareToMe": false
    }
  ]
}

```
The download and playback URLs are accessible via browser and require the password associated in the response.

If you want a direct download link, you can retrieve that from -	/v1/getRecordings/<recordingId>

As found in the above example with id": "724a81a697201039a976005056819cde

This will return a response like the following:

```javascript
{
  "id": "724a81a697201039a976005056819cde",
  "meetingId": "501e995485e2460bb129410116757b13_I_194316955237236650",
  "scheduledMeetingId": "501e995485e2460bb129410116757b13_20210514T203000Z",
  "meetingSeriesId": "501e995485e2460bb129410116757b13",
  "topic": "Test meeting-20210514 2025-1",
  "createTime": "2021-05-14T20:28:53Z",
  "siteUrl": "spouliottes-test.webex.com",
  "downloadUrl": "https://spouliottes-test.webex.com/spouliottes-test/lsr.php?RCID=77ab059a6b6512550d6a3ddafeea57aa",
  "playbackUrl": "https://spouliottes-test.webex.com/spouliottes-test/ldr.php?RCID=6197666928e747419d239f3cfdee3e49",
  "password": "tA3hwXUm",
  "temporaryDirectDownloadLinks": {
    "recordingDownloadLink": "https://nsj1wss.webex.com/nbr/MultiThreadDownloadServlet?siteid=13867087&recordid=220437037&confid=194316955237236650&from=MBS&trackingID=WEBEX-DEV-PORTAL_3bdadf4c-40a7-4ab5-967c-957c77a12a10_50&language=en_US&userid=600686172&serviceRecordID=220441022&ticket=SDJTSwAAAARjJiLHI3wKUisba87xO%2BurLcu84afdWTP4vg3ucK5ZhA%3D%3D&timestamp=1621283371277&islogin=yes&isprevent=no&ispwd=yes",
    "audioDownloadLink": "https://nsj1wss.webex.com/nbr/MultiThreadDownloadServlet/audio.mp3?siteid=13867087&recordid=220437037&confid=194316955237236650&from=MBS&trackingID=WEBEX-DEV-PORTAL_3bdadf4c-40a7-4ab5-967c-957c77a12a10_50&language=en_US&userid=600686172&serviceRecordID=220441022&ticket=SDJTSwAAAAS%2FF5Mw2d32msyLuoeJKubqgkKvTlrlXdzjrQdvVmQQ0Q%3D%3D&timestamp=1621283371276&islogin=yes&isprevent=no&ispwd=yes",
    "expiration": "2021-05-17T23:29:31Z"
  },
  "format": "MP4",
  "durationSeconds": 85,
  "sizeBytes": 4982263,
  "shareToMe": false
}
```
### Get the Transcripts – VTT and TXT format

You can now query for the transcripts using endpoint:-	/v1/meetingTranscripts/<meetingID>

A query might look like: https://webexapis.com/v1/meetingTranscripts?meetingId=501e995485e2460bb129410116757b13_I_194316955237236650

This will return to something like this:
```javascript
{
    "items": [
        {
            "id": "a5038f0b-320a-456f-a51f-7541eeb0eae5_M_501e995485e2460bb129410116757b13",
            "meetingId": "501e995485e2460bb129410116757b13_I_194316955237236650",
            "startTime": "2021-05-14T20:25:22Z",
            "vttDownloadLink": "https://webexapis.com/v1/meetingTranscripts/a5038f0b-320a-456f-a51f-7541eeb0eae5_M_501e995485e2460bb129410116757b13/download?meetingId=501e995485e2460bb129410116757b13_I_194316955237236650&format=vtt",
            "txtDownloadLink": "https://webexapis.com/v1/meetingTranscripts/a5038f0b-320a-456f-a51f-7541eeb0eae5_M_501e995485e2460bb129410116757b13/download?meetingId=501e995485e2460bb129410116757b13_I_194316955237236650&format=txt"
        }
    ]
}
```

### Get Assets in JSON format with speaker name
If you are designing an application that needs to programmatically use the transcript content, including speaker name in a machine readable format, you use the snippets API

-	meetingTranscripts/<transcriptId>/snippets
Note: Meeting host listing/getting/updating meeting transcript snippets function is behind on a feature toggle. Only EFT user can use this function. Please contact [Webex Support Team](https://developer.webex.com/support) to turn on the toggle.

The response body might be like the following:
```javascript
+ Response 200 (application/json;charset=UTF-8)
    + Attributes
        + items (array[SnippetObject], fixed-type) - Transcript snippet array
    + Body
            {
                "items": [
                    {
                        "id": "195d64646ad14be2924ea50f541fd91d_00001",
                        "text": "Hello everyone",
                        "personName": "John Andersen",
                        "personEmail": "john.andersen@example.com",
                        "offset": 1000,
                        "duration": 1500
                    }
                ]
            }
  ```
The offset field is the meeting start time in seconds. The ID field is a unique ID for the speaker slot.

### Set recording to on During a Meeting

The host of a meeting can toggle on recording, you can also ensure that all meetings have their recording enabled programmatically. When you receive a meeting creation notification, use the meeting ID to find the details of a meeting

The documentation for using the APIs can be found at https://developer.webex.com/docs/api/v1/meetings/list-meetings-of-a-meeting-series

The endpoint for meetings is:   /v1/meetings

To retrieve a meetings details, perform a Get to /vi/meetings with the meeting ID set in the request URI along with any optional parameters you choose. This would look like: https://webexapis.com/v1/meetings?meetingSeriesId=25bbf831-5be9-4c25-b4b0-9b592c8a086b&max=100&from=2019-03-18T09:30:00+08:00&to=2019-03-25T09:30:00+08:00&meetingType=%5Bobject%20Object%5D,%5Bobject%20Object%5D&state=%5Bobject%20Object%5D,%5Bobject%20Object%5D,%5Bobject%20Object%5D,%5Bobject%20Object%5D,%5Bobject%20Object%5D,%5Bobject%20Object%5D&isModified=false&hostEmail=john.andersen@example.com

```javascript
{
    "items": [
        {
            "id": "870f51ff287b41be84648412901e0402_20191101T120000Z",
            "meetingSeriesId": "870f51ff287b41be84648412901e0402",
            "meetingNumber": "123456789",
            "title": "Example Daily Meeting",
            "agenda": "Example Agenda",
            "password": "BgJep@43",
            "phoneAndVideoSystemPassword": "12345678",
            "meetingType": "scheduledMeeting",
            "state": "ready",
            "isModified": false,
            "timezone": "UTC",
            "start": "2019-11-01T12:00:00Z",
            "end": "2019-11-01T13:00:00Z",
            "hostUserId": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS9jN2ZkNzNmMi05ZjFlLTQ3ZjctYWEwNS05ZWI5OGJiNjljYzY",
            "hostDisplayName": "John Andersen",
            "hostEmail": "john.andersen@example.com",
            "hostKey": "123456",
            "siteUrl": "site4-example.webex.com",
            "webLink": "https://site4-example.webex.com/site4/j.php?MTID=md41817da6a55b0925530cb88b3577b1e",
            "sipAddress": "123456789@site4-example.webex.com",
            "dialInIpAddress": "192.168.100.100",
            "enabledAutoRecordMeeting": false,
            "allowAnyUserToBeCoHost": false,
            "enabledJoinBeforeHost": false,
            "enableConnectAudioBeforeHost": false,
            "joinBeforeHostMinutes": 0,
            "allowFirstUserToBeCoHost": false,
            "allowAuthenticatedDevices": false,
            "telephony": {
                "accessCode": "1234567890",
                "callInNumbers": [
                    {
                        "label": "US Toll",
                        "callInNumber": "123456789",
                        "tollType": "toll"
                    }
                ],
                "links": [
                    {
                        "rel": "globalCallinNumbers",
                        "href": "/api/v1/meetings/870f51ff287b41be84648412901e0402/globalCallinNumbers",
                        "method": "GET"
                    }
                ]
            }
        },

```
### Viewing the Log of the Participants

The meeting invite list can tell you who was invited, but it does not reveal who actually attended. Once a meeting is in progress or ended, you can query for a list of participants using: -	/v1/meetingParticipants

With meetingID as a query parameter, you can request this information as follows: https://webexapis.com/v1/meetingParticipants?meetingId=501e995485e2460bb129410116757b13_I_194316955237236650

This will return a response something like:

```javascript
{
    "items": [
        {
            "id": "870f51ff287b41be84648412901e0402_20191101T120000Z",
            "meetingSeriesId": "870f51ff287b41be84648412901e0402",
            "meetingNumber": "123456789",
            "title": "Example Daily Meeting",
            "agenda": "Example Agenda",
            "password": "BgJep@43",
            "phoneAndVideoSystemPassword": "12345678",
            "meetingType": "scheduledMeeting",
            "state": "ready",
            "isModified": false,
            "timezone": "UTC",
            "start": "2019-11-01T12:00:00Z",
            "end": "2019-11-01T13:00:00Z",
            "hostUserId": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS9jN2ZkNzNmMi05ZjFlLTQ3ZjctYWEwNS05ZWI5OGJiNjljYzY",
            "hostDisplayName": "John Andersen",
            "hostEmail": "john.andersen@example.com",
            "hostKey": "123456",
            "siteUrl": "site4-example.webex.com",
            "webLink": "https://site4-example.webex.com/site4/j.php?MTID=md41817da6a55b0925530cb88b3577b1e",
            "sipAddress": "123456789@site4-example.webex.com",
            "dialInIpAddress": "192.168.100.100",
            "enabledAutoRecordMeeting": false,
            "allowAnyUserToBeCoHost": false,
            "enabledJoinBeforeHost": false,
            "enableConnectAudioBeforeHost": false,
            "joinBeforeHostMinutes": 0,
            "allowFirstUserToBeCoHost": false,
            "allowAuthenticatedDevices": false,
            "telephony": {
                "accessCode": "1234567890",
                "callInNumbers": [
                    {
                        "label": "US Toll",
                        "callInNumber": "123456789",
                        "tollType": "toll"
                    }
                ],
                "links": [
                    {
                        "rel": "globalCallinNumbers",
                        "href": "/api/v1/meetings/870f51ff287b41be84648412901e0402/globalCallinNumbers",
                        "method": "GET"
                    }
                ]
            }
        },

```
