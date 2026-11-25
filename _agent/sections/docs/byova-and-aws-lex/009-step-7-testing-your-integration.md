---
type: Excerpt
canonical_url: https://developer.webex.com/docs/byova-and-aws-lex
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- 'Step 7: Testing Your Integration'
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/byova-and-aws-lex). [Full Markdown](../../../../docs/byova-and-aws-lex.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites](002-prerequisites.md)

## Article introduction

Transform your contact center with intelligent voice interactions using Webex Contact Center's BYOVA (Bring Your Own Virtual Agent) feature and AWS Lex.

## Selected section

## Step 7: Testing Your Integration

### 7.1 Set Up Agent Desktop

1. **Install Webex Contact Center Desktop**
   - Download from the Administrator Portal
   - Install on a test machine

2. **Log in as Agent**
   - Use the Premium Agent credentials from your provisioning email
   - Enter the extension number (1001)

3. **Set Agent Status to Available**
   - Ensure the agent is ready to receive calls

### 7.2 Test the Voice AI Integration

1. **Make a Test Call**
   - Call the entrypoint number from your provisioning email
   - You should hear the default greeting

2. **Interact with the Virtual Agent**
   - Speak naturally to test your AWS Lex bot
   - Try various utterances you configured
   - Test the conversation flow

3. **Test Agent Transfer**
   - Request to speak to a human agent
   - Verify the call transfers to your logged-in agent

### 7.3 Monitor the Integration

1. **Use the Monitoring Interface**
   - Open `http://localhost:8080` in your browser
   - Monitor active connections and session data

2. **Check Logs**
   - Review gateway logs for any errors
   - Check AWS CloudWatch logs for Lex activity

3. **Verify Audio Quality**
   - Test audio clarity and response times
   - Check audio recordings in `logs/audio_recordings/`

---
