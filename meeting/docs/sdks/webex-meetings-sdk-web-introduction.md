---
type: Guide
title: Web Meetings SDK | Introduction
display_title: Introduction
canonical_url: https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-introduction
content_type: documentation
product_group:
- webex-suite
categories:
- meeting
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-introduction)

This article provides a detailed introduction to the Webex Web SDK `meetings` object. It covers multiple methods and events related to meeting creation and retrieval.

## The Meetings Object

The `Meetings` instance is part of the Webex Meetings SDK that contains a list of meetings created using the SDK and APIs to perform specific operations or listen to certain events. A detailed explanation and code examples are provided in this article.

## Initialize a Meetings Object

After [importing and initializing the Web SDK](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-quickstart), the `Meetings` object is accessible from the `webex` object:

```js
const webex = new Webex.init();
const meetings = webex.meetings;
```

The `meetings` constant contains an instance of the Webex `Meetings` object.

## Register a Meeting Device

Once the `Meetings` object is instantiated, you can register a device using its `register()` method:

```js
const webex = new Webex.init();
await webex.meetings.register();
```



|              |                        |
| ------------ | ---------------------- |
| Asynchronous | Yes                    |
| Parameters   | No parameters required |
| Returns      | Promise\<undefined\>   |

## Create a Meeting

When registration has been completed, use the `Meetings` object's `create()` method to create a new `meeting` object:

```js
const meeting = await webex.meetings.create(destination, type);
```

The `create()` method particulars are detailed below:



<table style="width: 100%">
  <colgroup>
    <col style="width: 12%" />
    <col style="width: 88%" />
  </colgroup>
  <tbody>
    <tr>
      <td><strong>Asynchronous</strong></td>
      <td>Yes</td>
    </tr>
    <tr>
      <td><strong>Parameters</strong></td>
      <td>
        
          <table>
            <tbody>
              <tr>
                <th><strong>Sl. No</strong></th>
                <th colspan="1"><strong>Parameter Name</strong></th>
                <th><strong>Parameter Type</strong></th>
                <th><strong>Mandatory</strong></th>
                <th><strong>Description</strong></th>
              </tr>
              <tr>
                <td>1</td>
                <td><code>destination</code></td>
                <td><strong>String</strong></td>
                <td>Yes</td>
                <td>
                  The meeting destination where the meeting will take place. There are several possible types of destinations as described in the <code>type</code> parameter.
                </td>
              </tr>
              <tr>
                <td>2</td>
                <td><code>type</code></td>
                <td><strong>String</strong></td>
                <td>No</td>
                <td>
                  The meeting type must be one of the following:
                  <ul>
                    <li><strong>MEETING_LINK</strong></li>
                    <li><strong>SIP_URI</strong></li>
                    <li><strong>CONVERSATION_URL</strong></li>
                    <li><strong>PERSONAL_ROOM</strong></li>
                    <li><strong>MEETING_LINK</strong></li>
                  </ul>
                </td>
              </tr>
            </tbody>
          </table>
        
      </td>
    </tr>
    <tr>
      <td colspan="1"><strong>Returns</strong></td>
      <td colspan="1">Promise&lt;Meeting&gt;</td>
    </tr>
  </tbody>
</table>

The `Meetings` object returns a `meeting` object which can be used to perform actions on the meeting such as mute, unmute, switch audio, etc. 



> **Info**
>
> You can also directly create a meeting by using the `joinLink` or `startLink` parameters, which you can get from the [Join a Meeting API](https://developer.webex.com/docs/api/v1/meetings/join-a-meeting) response. While using the API, set the `createJoinLinkAsWebLink` or `createStartLinkAsWeblink` flag as true. Only then will you get the correct link. The link must then be set as the destination.



## Retrieve a List of All Meetings

You can create more than one meeting at a time. To obtain a list of all current meetings, use the `Meetings` object's `getAllMeetings()` method:

```js
const meetingList = webex.meetings.getAllMeetings();
```



|              |                          |
| ------------ | ------------------------ |
| Asynchronous | No                       |
| Parameters   | No parameters required   |
| Returns      | Map\<MeetingId,Meeting\> |

Here's an example of a returned list of meetings:

```json
{
  "3c9628aa-b51d-45c4-9166-1b9f7dafe95e" : { id: "3c9628aa-b51d-45c4-9166-1b9f7dafe95e", ...otherMeetingObjectAttributes },
  "c7d69b95-c9c6-40c1-9138-c6005b8be554": { id: "c7d69b95-c9c6-40c1-9138-c6005b8be554", ...otherMeetingObjectAttributesAndMethods },
}
```

## Synchronize Meetings from Webex Cloud

If your application is running on behalf of a registered Webex user, and that user has meetings running, you can use the `Meetings` object's `syncMeetings()` method to synchronize and then retrieve a list of those meetings.

```js
await webex.meetings.syncMeetings();
```



|              |                        |
| ------------ | ---------------------- |
| Asynchronous | Yes                    |
| Parameters   | No parameters required |
| Returns      | Promise\<undefined\>   |

After the `syncMeetings()` call is successful, use the `getAllMeetings` method to retrieve the list of meetings:

```js
await webex.meetings.syncMeetings();
const meetingList = webex.meetings.getAllMeetings();
```

## Fetch Meetings by Attribute

You can narrow down the list of meetings returned by choosing specific meeting attributes via the `getMeetingByType()` method.

For instance, to return a meeting whose `destination` property is https://cisco.webex.com/meet/alice:

```js
const meeting = webex.meetings.getMeetingByType(
  'destination',
  'https://cisco.webex.com/meet/alice'
);
```

The `getMeetingByType()` method particulars are detailed below:



<table>
  <colgroup>
    <col />
    <col />
  </colgroup>
  <tbody>
    <tr>
      <td><strong>Asynchronous</strong></td>
      <td>No</td>
    </tr>
    <tr>
      <td><strong>Parameters</strong></td>
      <td>
        
          <table>
            <tbody>
              <tr>
                <th><strong>Name</strong></th>
                <th><strong>Description</strong></th>
                <th><strong>Type</strong></th>
                <th><strong>Mandatory</strong></th>
              </tr>
              <tr>
                <td><code>attrib</code></td>
                <td>
                  The attribute of the meeting you'd like to retrieve, for instance,
                  <code>correlationId</code>, <code>destination</code>, <code>meetingLink</code>.
                </td>
                <td><strong>String</strong></td>
                <td>Yes</td>
              </tr>
              <tr>
                <td colspan="1"><code>value</code></td>
                <td colspan="1">
                    The value to be matched for the attribute.
                </td>
                <td colspan="1"><strong>String</strong></td>
                <td colspan="1">Yes</td>
              </tr>
            </tbody>
          </table>
        
      </td>
    </tr>
    <tr>
      <td colspan="1"><strong>Returns</strong></td>
      <td colspan="1"><strong>Object&lt;Meeting&gt;</strong></td>
    </tr>
  </tbody>
</table>

## Meetings Ready Event

A `meetings:ready` event fires when a `meetings` object is ready for use. A `meetings` object instance is ready once the containing `Webex` object is ready, and all the `meetings` object's instance parameters are set. You can subscribe to the ready event immediately following `Webex.init`:

```js
webex.meetings.on('meetings:ready',() => {
  console.log('Meetings object is ready for device registration');
  // Register a new device...
});
```

The ready event returns no payload. 



> **Info**
>
> Make any Meetings object method calls only after receiving this event.



## Meetings Registered Event

The `meetings:registered` event is emitted by a Meetings object after you call the  `register()` method:

```js
webex.meetings.on('meetings:registered',() => {
  console.log('Meetings object is ready to perform other operations');
  // Perform meeting operations such as create, sync, etc.
});
```

## Meeting is Added Event

The `meeting:added` event fires when a new `meeting` object is added to the `meetings` object:

```js
webex.meetings.on('meeting:added', ({ type, meeting }) => {
  // Perform operations on a specific meeting...
});
```

This event provides an object with two attributes in its payload:



<table>
  <colgroup>
    <col style="width: 10%" />
    <col style="width: 20%" />
    <col style="width: 70%" />
  </colgroup>
  <tbody>
    <tr>
      <th><strong>Sl. No</strong></th>
      <th><strong>Attribute Name</strong></th>
      <th><strong>Value</strong></th>
    </tr>
    <tr>
      <td>1</td>
      <td><code>type</code></td>
      <td>
        One of the following:
        
          <table>
            <tbody>
              <tr>
                <th><strong>Sl. No</strong></th>
                <th><strong>Type</strong></th>
                <th><strong>Description</strong></th>
              </tr>
              <tr>
                <td colspan="1">1</td>
                <td colspan="1"><strong>CREATED</strong></td>
                <td colspan="1">The meeting was created from within the SDK.</td>
              </tr>
              <tr>
                <td colspan="1">2</td>
                <td colspan="1"><strong>INCOMING</strong></td>
                <td colspan="1">A 1:1 meeting has been started with this user as the destination.</td>
              </tr>
              <tr>
                <td colspan="1">3</td>
                <td colspan="1"><strong>JOIN</strong></td>
                <td colspan="1">
                  A meeting has been started remotely and the current user is a participant. This is not a 1:1 meeting.
                </td>
              </tr>
            </tbody>
          </table>
        
      </td>
    </tr>
    <tr>
      <td colspan="1">2</td>
      <td colspan="1"><strong>meeting</strong></td>
      <td colspan="1">
        The Meeting object itself.
      </td>
    </tr>
  </tbody>
</table>

### Meeting is Removed Event

The `meeting:removed` event fires when a `meeting` object is removed from the `meetings` object:

```js
webex.meetings.on('meeting:removed', ({ meetingId, reason }) => {
  // Perform operations such as updating the UI to remove the defunct meeting...
});
```

This event returns an object with two of the following attributes as a payload:



<table>
  <thead>
    <th style="width: 5%"><strong>Sl. No</strong></th>
    <th style="width: 15%"><strong>Attribute Name</strong></th>
    <th style="width: 80%"><strong>Value<</strong>/th>
  </thead>
  <tbody>
    <tr>
      <td>1</td>
      <td>meetingId</td>
      <td>The Correlation ID of a meeting</td>
    </tr>
    <tr>
      <td>2</td>
      <td>reason</td>
      <td>
        <table>
            One of the following removal reasons:
          <thead>
            <th style="width: 10%"><strong>Sl. No</strong></th>
            <th style="width: 25%"><strong>Reason</strong></th>
            <th style="width: 65%"><strong>Description</strong></th>
          </thead>
          <tbody>
            <tr>
              <td>1</td>
              <td><strong>SELF_REMOVED</strong></td>
              <td>
                The server or a host removed the participant.
              </td>
            </tr>
            <tr>
              <td>2</td>
              <td><strong>MEETING_INACTIVE_TERMINATING</strong></td>
              <td>The meeting has ended or everyone has left.</td>
            </tr>
            <tr>
              <td>3</td>
              <td><strong>CLIENT_LEAVE_REQUEST</strong></td>
              <td>The participant triggered a leave meeting request.</td>
            </tr>
            <tr>
              <td>4</td>
              <td><strong>CLIENT_LEAVE_REQUEST_TAB_CLOSED</strong></td>
              <td>
                The participant triggered a leave meeting request by closing the
                browser tab.
              </td>
            </tr>
            <tr>
              <td>5</td>
              <td><strong>NO_MEETINGS_TO_SYNC</strong></td>
              <td>
                A meeting has been created locally but doesn't exist in
                the cloud server upon trying to sync meetings using <code>syncMeetings()</code>. 
              </td>
            </tr>
            <tr>
              <td>6</td>
              <td><strong>MEETING_CONNECTION_FAILED</strong></td>
              <td>
                The meeting failed to connect due to ICE candidate failures or
                firewall issues.
              </td>
            </tr>
          </tbody>
        </table>
      </td>
    </tr>
  </tbody>
</table>

## Network Disconnected Event

The `network:disconnected` event fires when a meeting instance is disconnected from the Webex Cloud server or when the browser's local network is disconnected:

```js
webex.meetings.on('network:disconnected', () => {
  // Perform operations to cleanup the UI that is related to a Meeting Leave
});
```

### Network Connected Event

The `network:connected` event fires when the meetings instance is reconnected to the network after being disconnected:

```js
webex.meetings.on('network:connected', () => {
  //Perform operations to reconnect Meeting
});
```
