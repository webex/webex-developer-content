---
type: Excerpt
canonical_url: https://developer.webex.com/docs/bring-your-own-virtual-agent
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Phase 4 - Integrating Data Source
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/bring-your-own-virtual-agent). [Full Markdown](../../../../docs/bring-your-own-virtual-agent.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Phase 2 - Authentication](003-phase-2-authentication.md)

## Article introduction

As part of the "Bring Your Own" (BYO) initiative, Webex Contact Center aims to enable seamless integrations with third-party AI providers, enhancing the Webex customer experience with cutting-edge AI innovations. Bring your own Virtual Agent is the first slice of all other other AI functionalities you can bring to Webex Contact Center product offerings.

## Selected section

## Phase 4 - Integrating Data Source

Once the data source is registered, you can integrate it into your contact center configuration:

1. **Config creation**:
   Navigate to **Main Menu -> Contact Center -> Integration -> Features** to create a new CCAI Config:

   
   ![CCAI Config](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltce69626ab2415ccf/2.png)

   

2. **Flow Creation**:
    Create a flow with the Virtual Agent Voice Activity and use the AI configuration you created above in the Flow Control UI.

   
      ![Flow Designer](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt4ebb66c23612b9c4/3.png)


3. **Entry Point Mapping**:
     Map the EntryPoint to the newly created flow (**Contact Center -> Channels -> Entry Point**)

   
   ![Entry Point Mapping](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltef4256ccec99389b/4.png)


After these steps, make a call to the phone number specified in the entry point via your cell phone or [Webex Calling Extension for Chrome](https://help.webex.com/en-us/article/a5ormz/Webex-Calling-for-Chrome) if you are not in the US or Canada.
