---
type: Excerpt
canonical_url: https://developer.webex.com/docs/byova-and-aws-lex
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- 'Step 4: Configuring the BYOVA Gateway'
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/byova-and-aws-lex). [Full Markdown](../../../../docs/byova-and-aws-lex.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites](002-prerequisites.md)

## Article introduction

Transform your contact center with intelligent voice interactions using Webex Contact Center's BYOVA (Bring Your Own Virtual Agent) feature and AWS Lex.

## Selected section

## Step 4: Configuring the BYOVA Gateway

### 4.1 Clone and Set Up the Gateway

1. **Clone the Repository**

   ```bash
   git clone https://github.com/webex/webex-byova-gateway-python.git
   cd webex-byova-gateway-python
   ```

2. **Create Virtual Environment**

   ```bash
   # Create virtual environment
   python -m venv venv
   
   # Activate virtual environment (REQUIRED)
   # On macOS/Linux:
   source venv/bin/activate
   # On Windows:
   # venv\Scripts\activate
   
   # Verify activation - you should see (venv) in your prompt
   which python  # Should show path to venv/bin/python
   ```

3. **Install Dependencies**

   ```bash
   pip install -r requirements.txt
   ```

4. **Generate gRPC Stubs**

   ```bash
   python -m grpc_tools.protoc -I./proto --python_out=src/generated --grpc_python_out=src/generated proto/*.proto
   ```

### 4.2 Configure AWS Lex Connector

1. **Set AWS Credentials**

   ```bash
   # Set environment variables (recommended for production)
   export AWS_ACCESS_KEY_ID=your_access_key_here
   export AWS_SECRET_ACCESS_KEY=your_secret_key_here
   export AWS_DEFAULT_REGION=us-east-1
   ```

2. **Configure JWT Validation**

   JWT validation secures communication with Webex Contact Center. Configure it with your public URL from Step 3.

   Edit `config/config.yaml` and add/update the JWT section:

   ```yaml
   # JWT validation configuration for gRPC requests
   jwt_validation:
     # Enable JWT validation (required for production)
     enabled: true
     
     # Enforce validation - set false only for initial testing
     enforce_validation: true
     
     # Your public URL from Step 3 (no port number!)
     # This MUST exactly match your BYoDS registration in Step 5.3
     # 
     # Examples:
     #   ngrok: https://abc123def456.ngrok-free.app
     #   production: https://byova-gateway.yourcompany.com
     datasource_url: "https://YOUR_PUBLIC_URL_FROM_STEP_3"
     
     # Standard BYOVA schema UUID (do not change)
     datasource_schema_uuid: "5397013b-7920-4ffc-807c-e8a3e0a18f43"
     
     # Public key cache duration
     cache_duration_minutes: 60
   ```

   **Critical URL Matching Rule**:

   - The `datasource_url` here must EXACTLY match your BYoDS registration (Step 5.3)
   - Use the same URL in both places - no port number needed
   - Example: `https://abc123.ngrok-free.app` (not `https://abc123.ngrok-free.app:50051`)

   **For Development/Testing Only**:

   ```yaml
   jwt_validation:
     enabled: false  # Disable JWT temporarily for local testing
   ```

   ⚠️ **Warning**: Never disable JWT in production!

3. **Update Configuration File**

   Edit `config/config.yaml`:

   ```yaml
   # Gateway settings
   gateway:
     host: "0.0.0.0"
     port: 50051

   # JWT validation configuration
   jwt_validation:
     enabled: true
     enforce_validation: true
     # Your public URL from Step 3 (no port!)
     datasource_url: "https://YOUR_PUBLIC_URL"
     datasource_schema_uuid: "5397013b-7920-4ffc-807c-e8a3e0a18f43"
     cache_duration_minutes: 60

   # Monitoring interface
   monitoring:
     enabled: true
     host: "0.0.0.0"
     port: 8080

   # Connectors
   connectors:
     # AWS Lex Connector
     aws_lex_connector:
       type: "aws_lex_connector"
       class: "AWSLexConnector"
       module: "connectors.aws_lex_connector"
       config:
         region_name: "us-east-1"  # Your AWS region
         # Initial trigger text sent when starting a conversation (default: "hello")
         # For Bedrock agents, use a simple greeting rather than a specific request
         # to avoid triggering function calls before the agent is ready
         initial_trigger_text: "hello"
         barge_in_enabled: false
         audio_logging:
           enabled: true
           output_dir: "logs/audio_recordings"
           filename_format: "{conversation_id}_{timestamp}_{source}.wav"
           log_all_audio: true
           max_file_size: 10485760
           sample_rate: 8000
           bit_depth: 8
           channels: 1
           encoding: "ulaw"
         agents: []
   ```

### 4.3 Start the Gateway

1. **Start the Server**

   ```bash
   # Ensure virtual environment is activated
   source venv/bin/activate
   
   # Start the gateway
   python main.py
   ```

2. **Verify Startup**

   - You should see output indicating both gRPC and web servers are running
   - Check the monitoring interface at `http://localhost:8080`

3. **Test Gateway Status**

   ```bash
   # Test the API
   curl http://localhost:8080/api/status
   
   # Check available agents
   curl http://localhost:8080/api/agents
   ```

---
