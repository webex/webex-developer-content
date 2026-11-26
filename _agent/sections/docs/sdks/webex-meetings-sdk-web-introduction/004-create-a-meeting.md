---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-introduction
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Create a Meeting
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-introduction). [Full Markdown](../../../../../docs/sdks/webex-meetings-sdk-web-introduction.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article provides a detailed introduction to the Webex Web SDK `meetings` object. It covers multiple methods and events related to meeting creation and retrieval.

## Selected section

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
