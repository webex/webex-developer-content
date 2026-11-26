---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-introduction
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Fetch Meetings by Attribute
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-introduction). [Full Markdown](../../../../../docs/sdks/webex-meetings-sdk-web-introduction.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article provides a detailed introduction to the Webex Web SDK `meetings` object. It covers multiple methods and events related to meeting creation and retrieval.

## Selected section

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
