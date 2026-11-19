---
type: Excerpt
canonical_url: https://developer.webex.com/docs/cc-web-widgets-components-callcontrolcad
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Usage Example
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/cc-web-widgets-components-callcontrolcad). [Full Markdown](../../../../docs/cc-web-widgets-components-callcontrolcad.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

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

## Selected section

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
