---
type: Excerpt
canonical_url: https://developer.webex.com/docs/byova-and-aws-lex
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- 'Step 6: Import and Configure Flow'
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/byova-and-aws-lex). [Full Markdown](../../../../docs/byova-and-aws-lex.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites](002-prerequisites.md)

## Article introduction

Transform your contact center with intelligent voice interactions using Webex Contact Center's BYOVA (Bring Your Own Virtual Agent) feature and AWS Lex.

## Selected section

## Step 6: Import and Configure Flow

### 6.1 Import the BYOVA Flow Template

![Lex Flow](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltaf25122e86a044fb/68f7f9f60f1176b0b037cc07/aws-lex-01-flow.png?branch=integration)

1. **Navigate to Control Hub**
   - Go to [https://admin.webex.com/login](https://admin.webex.com/login)
   - Sign in with your administrator credentials from the provisioning email

2. **Access Contact Center Flows**
   - In Control Hub, navigate to **Contact Center**
   - Click on **Flows**
   - Select **Manage Flows**
   - Click **Import Flow**

   **Reference**: For detailed information about Flow Designer and flow management, see the [Build and manage flows with Flow Designer documentation](https://help.webex.com/en-us/article/nhovcy4/Build-and-manage-flows-with-Flow-Designer#Cisco_Task.dita_0e76fcdd-29a3-47c3-8544-f6613dfeb8f0).

3. **Import the BYOVA Flow Template**
   - Download the [`BYOVA_Gateway_Flow.json`](https://github.com/Webex/webex-byova-gateway-python/blob/main/BYOVA_Gateway_Flow.json) file from the gateway repository 
   - In the import dialog, choose the `BYOVA_Gateway_Flow.json` file
   - The flow will be imported with the name "BYOVA"

4. **Configure the Virtual Agent**
   - In the imported flow, locate the **VirtualAgentV2_q2c** activity
   - Click on the activity to open its properties
   - Update the **Virtual Agent** selection:
     - **Connector Name**: Select your BYOVA connector (e.g., "AWS Lex Connector")
     - **Virtual Agent ID**: Select your configured virtual agent
   - Save the activity configuration

5. **Review Flow Structure**

   The imported flow includes:

   - **Start**: Entry point for calls
   - **Virtual Agent**: Routes to your BYOVA virtual agent
   - **Decision Logic**: Handles agent disconnection and transfer scenarios
   - **Play Message**: Provides feedback to callers
   - **End**: Terminates the call

6. **Save and Activate the Flow**

   - Save your flow configuration
   - Activate the flow for testing

### 6.2 Assign Flow to Entry Point

1. **Navigate to Channels**
   - In Control Hub, go to **Contact Center** → **Channels**
   - Select **Entry Point 1** (or your configured entry point)

2. **Configure Entry Point Routing**
   - In the Entry Point 1 configuration, locate the **Routing Flow** setting
   - Change the routing flow from the default to your **BYOVA** flow
   - Save the configuration

3. **Verify Assignment**
   - Confirm that Entry Point 1 is now using the BYOVA flow
   - The entry point will now route calls through your virtual agent integration

---
