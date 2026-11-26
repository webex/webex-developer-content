---
type: Excerpt
canonical_url: https://developer.webex.com/docs/cc-web-widgets-components-callcontrolcad
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Features
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
