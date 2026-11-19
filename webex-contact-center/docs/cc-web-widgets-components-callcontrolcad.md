---
type: Guide
title: Webex Contact Center Web Widgets | Components | CallControlCAD
display_title: Overview
canonical_url: https://developer.webex.com/docs/cc-web-widgets-components-callcontrolcad
content_type: documentation
product_group:
- webex-contact-center
categories:
- webex-contact-center
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/cc-web-widgets-components-callcontrolcad)

The `CallControlCAD` component provides advanced call controls with Call Associated Data (CAD), including consult and transfer capabilities.

---

CallControlCAD extends basic call control functionality with advanced features for complex call scenarios. It includes:

 1. All standard call controls (hold, resume, end, wrap-up)
 2. Consult functionality
 3. Call transfer capabilities
 4. Three-party and Multi-party conference capabilities
 5. Call Associated Data (CAD) display

**Look and feel**:

1. ![1-cc-cad.png](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte6b2207d584d9b06/6972a3360398572e10825dfe/1-cc-cad.png?branch=integration&width=560)
2. ![2-cc-cad.png](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt9c5d71c57f056f0c/6972a336bc2c09fed6d53fa6/2-cc-cad.png?branch=integration&width=560)
3. ![3-cc-cad.png](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltab06d00be4e373ed/6972a33623d5fb3510c77de4/3-cc-cad.png?branch=integration&width=560)
4. ![4-cc-cad.png](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt96480b54396b91cb/6972a336aa1918f88f309326/4-cc-cad.png?branch=integration&width=560)
5. ![5-cc-cad.png](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blta5ec13acc113c954/6972a336237b3d74d53a3bad/5-cc-cad.png?branch=integration&width=560)
6. ![6-cc-cad.png](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt44381db9c0666400/6972a33682162957e7931245/6-cc-cad.png?branch=integration&width=560)
7. ![7-cc-cad.png](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt5258bdb80f2da192/6972a336c407ff863a7cb5f4/7-cc-cad.png?branch=integration&width=560)
8. ![8-cc-cad.png](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltcebf11e0eb0ad6d2/6972a336035501b0fe69538b/8-cc-cad.png?branch=integration&width=560)
9. ![9-cc-cad.png](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltd725d696f4b58580/6972a336821629f8e5931241/9-cc-cad.png?branch=integration&width=560)
10. ![10-cc-cad.png](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltd3b1a5bf12adaeb1/6972a3360398573a6b825dfc/10-cc-cad.png?branch=integration&width=560)

## Import

```js
import { CallControlCAD } from '@webex/cc-widgets';
```

## Props

| Prop                          | Type                               | Required | Default | Description                                                                        |
| ----------------------------- | ---------------------------------- | -------- | ------- | ---------------------------------------------------------------------------------- |
| `onHoldResume`                | `({isHeld, task}) => void`         | No       | -       | Callback function triggered when hold/resume action is performed                   |
| `onEnd`                       | `({ task }) => void`               | No       | -       | Callback function triggered when a call is ended                                   |
| `onWrapUp`                    | `({ task, wrapUpReason }) => void` | No       | -       | Callback function triggered when wrap-up is initiated with task details and reason |
| `onRecordingToggle`           | `({ isRecording, task }) => void`  | No       | -       | Callback function triggered when recording is toggled (paused or resumed)          |
| `onToggleMute`                | `({isMuted, task}) => void`        | No       | -       | Callback function triggered when the call is muted or unmuted                      |
| `callControlClassName`        | `string`                           | No       | -       | Custom CSS class name for the main call control component                          |
| `callControlConsultClassName` | `string`                           | No       | -       | Custom CSS class name for the consult control component                            |

## Usage Example

Widget

```js
<CallControlCAD
  onHoldResume={handleHoldResume}
  onEnd={handleEnd}
  onWrapUp={handleWrapUp}
  onRecordingToggle={onRecordingToggle}
  onToggleMute={onToggleMute}
  callControlClassName="custom-call-control"
  callControlConsultClassName="custom-consult-control"
/>
```

Callback

```js
const handleHoldResume = ({ isHeld, task }) => {
  console.log('Hold/Resume action triggered in CAD', { isHeld, task });
};

const handleEnd = ({ task }) => {
  console.log('Call ended in CAD', { task });
};

const handleWrapUp = ({ task, wrapUpReason }) => {
  console.log('Wrap-up initiated in CAD:', { task, wrapUpReason });
};

const onRecordingToggle = ({ isRecording, task }) => {
  console.log('Recording toggled', { isRecording, task });
};

const onToggleMute = ({ isMuted, task }) => {
  console.log('onToggleMute invoked', { isMuted, task });
};
```

Custom Styles

```css
.custom-call-control,
.custom-consult-control {
  padding: 20px;
  border: rgba(204, 204, 204, 0.5) 1px solid;
  box-shadow: 0 0 10px rgba(204, 204, 204, 0.5);
  border-radius: 5px;
  margin: 20px;
}
```

## Features

### Standard Call Controls

- **Hold/Resume**: Place calls on hold and resume them
- **End Call**: Terminate the current call
- **Wrap-Up**: Complete after-call work with disposition codes
- **Recording Toggle**: Allows agents to pause and resume recording

### Advanced Features

#### Consult

Consult with a supervisor or another agent before transferring:

- Initiate consult call while keeping original caller on hold
- Discuss customer situation privately
- Return to original call or proceed with transfer

#### Transfer

Transfer calls to other agents, queues, or external numbers:

- **Blind Transfer**: Transfer immediately without consultation
- **Consult-Transfer**: Consult first, then transfer
- Transfer to specific agents or skill groups

#### Conference

The conference feature allows agents to create multi-party calls by bringing together multiple participants.

**Conference Types:**

- **Three-Party Conference**: Agent, original caller, and one additional participant
- **Multi-Party Conference**: Agent and multiple participants in a single call session

**Conference Capabilities:**

- Initiate conference after establishing a consult call
- Add multiple participants to an ongoing call sequentially
- End conference or exit as an individual participant

## Call Workflows

### Consult-Transfer Workflow

1. Agent receives call
2. Agent clicks Consult and chooses another agent, queue, a contact from the address book, or dials a PSTN number
3. Consult call is established (original caller on hold)
4. Agent discusses with consultant
5. Agent clicks Transfer to complete

### Blind Transfer Workflow

1. Agent receives call
2. Agent chooses a transfer destination such as another agent, queue, a contact from the address book, or dials a PSTN number
3. Agent clicks Transfer
4. Call is immediately transferred

### Conference Workflow

**Three-Party Conference:**

1. Agent receives call from customer
2. Agent clicks Consult and selects another agent, queue, or dials a number
3. Consult call is established (original caller on hold)
4. Agent clicks Conference to join all parties
5. Three-way call is active with agent, customer, and consultant

**Multi-Party Conference:**

1. Agent has an active call or conference in progress
2. Agent can add additional participants by repeating the consult process
3. Each new participant joins the existing conference
4. All parties can communicate simultaneously
5. Agent can exit or end the conference

## Configuration Notes

- The component requires an active call to display controls
- The `store` must be initialized with a valid access token
- Agent must be logged in with a station
- Transfer destinations must be configured in the contact center system
- Make sure to wrap the component with `ThemeProvider` and `IconProvider` from Momentum Design
- `callControlClassName` and `callControlConsultClassName` classes and defining styles for it are required for proper UI

## Known Issues

- Styling issues may occur with certain CSS frameworks - use custom class names to override
- DNIS value should be displayed alongside phone number in some configurations
