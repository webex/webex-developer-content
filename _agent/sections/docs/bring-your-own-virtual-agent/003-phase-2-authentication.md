---
type: Excerpt
canonical_url: https://developer.webex.com/docs/bring-your-own-virtual-agent
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Phase 2 - Authentication
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/bring-your-own-virtual-agent). [Full Markdown](../../../../docs/bring-your-own-virtual-agent.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

As part of the "Bring Your Own" (BYO) initiative, Webex Contact Center aims to enable seamless integrations with third-party AI providers, enhancing the Webex customer experience with cutting-edge AI innovations. Bring your own Virtual Agent is the first slice of all other other AI functionalities you can bring to Webex Contact Center product offerings.

## Selected section

## Phase 2 - Authentication 

Authentication is set up using “Bring Your Own Data Source,” which gives developers the flexibility to register a unique URL and a token for every customer they onboard. Developers can create a Service App to start using the Voice Voice Agent schema.

**Service App creation and authorization**

**Step 1:** Login to the developer portal via a sandbox user credentials (You can recreate a service app later in your official webex account). Create a Service app with `spark-admin:dataSource_read/dataSource_write` scopes.

 ![image](https://github.com/user-attachments/assets/e9fa0edc-6364-4c49-b5a1-21b8f139b10c)
 
**Step 2:** For connecting to your Voice Virtual Agent application, choose the voice virtual agent schema in the "Data Sources" section. Also add the domain of the URL to which the connection should be established in the "Data Exchange Domain. For Eg. if the connection must be established for the URL (`www.virtualagent.cisco.com`), enter (`cisco.com`) :

![image](https://github.com/user-attachments/assets/04b7e964-c7c5-4e9d-a31e-29ed32073958)

**Step 3:** After creation, you need to submit your app to the customer org admin for authorization:

 ![image](https://github.com/user-attachments/assets/6740d22c-24d7-4685-b407-8c62a24362b4)

**Important Links** 
1. [Service Apps](https://developer.webex.com/docs/service-apps)
2. [Bring Your Own Data Source](https://developer.webex.com/docs/bring-your-own-datasource)
3. [BYODS SDK](https://www.npmjs.com/package/@webex/byods)
4. [Demo of Bring your own Data Source](https://app.vidcast.io/share/bce964f2-4162-4467-9538-af5570176933)
