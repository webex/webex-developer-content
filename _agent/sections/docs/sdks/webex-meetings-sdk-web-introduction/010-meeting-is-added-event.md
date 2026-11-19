---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-introduction
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Meeting is Added Event
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-introduction). [Full Markdown](../../../../../docs/sdks/webex-meetings-sdk-web-introduction.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article provides a detailed introduction to the Webex Web SDK `meetings` object. It covers multiple methods and events related to meeting creation and retrieval.

## Selected section

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
