---
type: Excerpt
canonical_url: https://developer.webex.com/docs/bring-your-own-virtual-agent
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Phase 3 - Data Source Registration
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/bring-your-own-virtual-agent). [Full Markdown](../../../../docs/bring-your-own-virtual-agent.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Phase 2 - Authentication](003-phase-2-authentication.md)

## Article introduction

As part of the "Bring Your Own" (BYO) initiative, Webex Contact Center aims to enable seamless integrations with third-party AI providers, enhancing the Webex customer experience with cutting-edge AI innovations. Bring your own Virtual Agent is the first slice of all other other AI functionalities you can bring to Webex Contact Center product offerings.

## Selected section

## Phase 3 - Data Source Registration

To use the service app created, follow these onboarding steps:

1. **Org admin authorization**:
   A user with organization or contact center admin role (you can login to (`www.admin.webex.com`) with the admin credentials of your sandbox) needs to authorize the app by going to **Control Hub -> Apps**.


   ![Service App](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte2e64bb836a5ddb6/1.png)

2. **Generate Service App Token**:
   As the provider, you must generate an access token for the authorized service app. Navigate to your service app in the developer portal and choose **Generate Token** for the customer org by selecting the org from the dropdown menu.

3. **Register Data Source**:
   Using the generated token, register your data source by making a POST request to the dataSources API:

   ```bash
   POST https://webexapis.com/v1/dataSources
   ```

   Include the following fields in your request body:
   - `name`: Unique identifier for the data source
   - `displayName`: Human-readable name
   - `url`: Your Virtual Agent endpoint URL
   - `authToken`: Authentication token (nonce) for secure communication
   - `providerId`: Your service app's provider ID
   - `schema`: Voice Virtual Agent schema ID (`5397013b-7920-4ffc-807c-e8a3e0a18f43`)
   - `state`: Set to `ACTIVE` to enable the data source

   For detailed API documentation, refer to the [Data Sources API](https://developer.webex.com/docs/api/v1/data-sources).
