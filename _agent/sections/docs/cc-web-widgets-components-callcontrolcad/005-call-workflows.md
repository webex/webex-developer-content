---
type: Excerpt
canonical_url: https://developer.webex.com/docs/cc-web-widgets-components-callcontrolcad
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Call Workflows
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
