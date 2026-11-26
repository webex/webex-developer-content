---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-call-control
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Desktop Actions
- sendDtmf(dtmfData)
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/desktop-call-control). [Full Markdown](../../../../docs/desktop-call-control.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before You Begin](001-before-you-begin.md)

## Article introduction

Retrieve tasks and control interactions, WebRTC calls, and call recording from Desktop widgets.

## Parent context

## Desktop Actions

The `Desktop.actions` module retrieves data and performs actions for Desktop widgets.

## Selected section

### sendDtmf(dtmfData)

Sends Dual-Tone Multi-Frequency (DTMF) signals during an active call. DTMF tones are used to interact with Interactive Voice Response (IVR) systems, access voicemail systems, or navigate automated phone menus. Each tone corresponds to a specific digit or symbol on a telephone keypad.

**Example**

```javascript
// Send a single digit
await Desktop.agentContact.sendDtmf("5");

// Send multiple digits for a PIN or extension
await Desktop.agentContact.sendDtmf("1234");

// Send special characters
await Desktop.agentContact.sendDtmf("*");
await Desktop.agentContact.sendDtmf("#");

// Send a sequence for navigating an IVR menu
await Desktop.agentContact.sendDtmf("2*9876#");
```

**Parameters**

| Name     | Type   | Description                                                                                           | Required |
| -------- | ------ | ----------------------------------------------------------------------------------------------------- | -------- |
| dtmfData | String | The DTMF tone(s) to send. Valid characters: 0-9, *, #. Can be a single character or a sequence.     | Yes      |
