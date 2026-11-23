---
type: Excerpt
canonical_url: https://developer.webex.com/docs/byova-and-aws-lex
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- 'Step 1: Setting Up Your Webex Contact Center Sandbox (Optional)'
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/byova-and-aws-lex). [Full Markdown](../../../../docs/byova-and-aws-lex.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites](002-prerequisites.md)

## Article introduction

Transform your contact center with intelligent voice interactions using Webex Contact Center's BYOVA (Bring Your Own Virtual Agent) feature and AWS Lex.

## Selected section

## Step 1: Setting Up Your Webex Contact Center Sandbox (Optional)

> **Skip this step if**: You already have access to a Webex Contact Center organization. If you do, jump to section 1.4 to ensure BYOVA is enabled.

### 1.1 When You Need a Sandbox

Request a sandbox if:

- This is your first time using Webex Contact Center
- You need a fresh environment for testing BYOVA
- You don't have access to any WxCC organization

### 1.2 When to Skip This Step

Skip if:

- You already have admin access to a WxCC organization
- You have a production WxCC environment for testing
- You've previously set up a sandbox that's still active

If you're skipping, **continue to section 1.4** to verify BYOVA is enabled.

### 1.3 Request a Sandbox

1. **Sign in to Webex Developer Portal**
   - Go to [developer.webex.com](https://developer.webex.com)
   - Sign in with your Webex account

2. **Navigate to Contact Center Sandbox**
   - Go to [Contact Center Sandbox](https://developer.webex.com/create/docs/sandbox_cc)
   - Click **"Request a Sandbox"**

3. **Complete the Request Process**
   - Read and accept the Terms and Conditions
   - Check "By creating this app, I accept the Terms of Service"
   - Click **"Request a Sandbox"**

4. **Wait for Provisioning**
   - Sandbox creation takes up to 15 minutes
   - You'll receive several emails with account details
   - **Save the final provisioning email** - it contains critical information

Your provisioning email will contain:

**Administrator Account:**

- **Username**: `admin@xxxxxx-xxxx.wbx.ai`
- **Password**: `********`
- **Webex Site URL**: `xxxxxx-xxxx.webex.com`

**Agent Accounts:**

- **Premium Agent**: `user1@xxxxxx-xxxx.wbx.ai` (Extension: 1001)
- **Supervisor Agent**: `user2@xxxxxx-xxxx.wbx.ai` (Extension: 1002)

**Phone Numbers:**

- **Main PSTN Number**: `+1nnnnnnnnnn` (for Webex calling)
- **Entrypoint Number**: `+1nnnnnnnnnn` (for Contact Center)

1. **Open a Private/Incognito Browser Window**
   - Chrome: `Ctrl+Shift+N` (Windows) or `Cmd+Shift+N` (Mac)
   - Firefox: `Ctrl+Shift+P` (Windows) or `Cmd+Shift+P` (Mac)

2. **Navigate to the Administrator Portal**
   - Go to [https://admin.webex.com](https://admin.webex.com)
   - Enter your administrator email and password from the provisioning email

3. **Verify Access**
   - You should see the Webex Contact Center Administrator Portal
   - Note the site configuration and available features

### 1.4 Request the BYOVA Feature (Required for All Users)

> **Important**: Whether you're using a sandbox or existing organization, you need BYOVA enabled.

1. **Copy your Organization ID**
   - In the Administrator Portal, navigate to **Settings** → **Organization**
   - Copy the Organization ID

2. **Submit a Developer Support Ticket**
   - Go to the [Webex Developer Support](https://developer.webex.com/support) page.
   - Click **"Contact Support"** and fill out the ticket.
     - Subject: Request to Enable BYOVA Feature for Webex Contact Center Sandbox
     - Description:
       - Hello Webex Developer Support Team,
       - I would like to request the activation of the **BYOVA (Bring Your Own Virtual Agent)** feature for my Webex Contact Center sandbox environment.
       - **Organization Name:** ACME Test Org
       - **Organization ID:** `your-organization-id-here`
       - **Sandbox Email Used for Request:** `admin@xxxxxx-xxxx.wbx.ai`
       - **Sandbox URL:** `https://xxxxxx-xxxx.webex.com`
       - This feature is required to continue development and testing for virtual agent integrations. Please let me know if you need any additional information.
   - Wait for confirmation from the support team. You'll receive an email when BYOVA is enabled for your org.

---
