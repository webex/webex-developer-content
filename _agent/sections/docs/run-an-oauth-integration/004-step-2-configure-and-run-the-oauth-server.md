---
type: Excerpt
canonical_url: https://developer.webex.com/docs/run-an-oauth-integration
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- 'Step 2: Configure and Run the OAuth Server'
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/run-an-oauth-integration). [Full Markdown](../../../../docs/run-an-oauth-integration.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites](002-prerequisites.md)

## Article introduction

This tutorial shows you how to get a Node.js server running locally that acts as an OAuth client for a Webex [integration](https://developer.webex.com/docs/integrations), obtain an API access token for the authenticating user, and uses it to call a Webex API to get information about the user.

## Selected section

## Step 2: Configure and Run the OAuth Server

To install the server locally you clone an existing [Webex OAuth sample](https://github.com/WebexSamples/webex-oauth-integration) and install the project's dependencies. You also configure the app's .env file with the OAuth's client secret and authorization URL copied from the integration's settings page.

**To run the server locally:**

1. Clone the OAuth sample project and install its dependencies.

    ```bash
    git clone https://github.com/WebexSamples/webex-oauth-integration.git
    cd webex-integration-sample
    npm install
    ```

2. Open the project's **.env** file and paste your integration's client secret and initial authorization URL that you copied from the integration's configuration page.

    * Add your client ID and secret to the corresponding environment variables.

    ```plain
    # Your OAuth integration's client ID/secret
    CLIENT_SECRET=<INTEGRATION CLIENT SECRET>
    
    # Initial authorization URL
    AUTH_INIT_URL=<AUTH URL>
    ```

3. Save your changes to the server.js and .env files and start the server from a terminal.

    ```bash
    node server.js
    ```

    The output shows the OAuth client's configuration.

    ```plain
    Debugger attached.
    oauth OAuth integration settings:
    oauth    - CLIENT_ID    : C909b987b64167258774e532d595702ef864a35f7614678dbe4046056daf67d63
    oauth    - REDIRECT_URI : http://localhost:8080/oauth
    oauth    - SCOPES       : spark:people_read +0ms
    Webex OAuth Integration started on http://localhost:8080
    ```
