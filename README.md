# n8n Workflow Generation

An n8n workflow generation agent that transforms natural language descriptions into production-ready n8n workflows.

## How It Works

```
1. Prompt Claude Code    →    2. Agent generates files    →    3. Copy to n8n
                                                                      ↓
                              5. Execute hook             ←    4. Get webhook URL
                                      ↓
                              Workflow runs & returns result
```

## Step-by-Step Usage

### Step 1: Prompt Claude Code Agent
Describe the workflow you want in natural language:
```
"Create a workflow that receives a message, processes it with AI, and returns the response"
```

### Step 2: Agent Generates Files
Claude Code will create:
- `workflows/` - Workflow JSON to import
- `prompts/` - System prompts for AI nodes
- `code/` - Code snippets for Code nodes
- `hooks/` - Script to trigger the workflow

### Step 3: Copy to n8n Interface
1. Import the workflow JSON into n8n
2. Open AI Agent nodes → paste prompts from `prompts/`
3. Open Code nodes → paste code from `code/`
4. Activate the workflow

### Step 4: Get Webhook URL
After activating the workflow in n8n:
1. Click on the Webhook node
2. Copy the **Production URL**
3. Update the URL in the corresponding `hooks/` script

### Step 5: Execute Hook
Run the hook script to trigger your workflow:
```bash
./hooks/your-workflow.sh
```
The workflow executes and returns the result.

## Project Structure

```
├── hooks/             # Scripts to trigger workflows
├── prompts/           # System prompts for AI Agent nodes
├── code/
│   ├── javascript/    # JavaScript for Code nodes
│   └── python/        # Python for Code nodes
├── workflows/         # Workflow JSON files
└── CLAUDE.md          # Agent instructions
```

## Workflow Design

All generated workflows follow this pattern:
- **Start**: Webhook node (receives trigger)
- **End**: Webhook Response node (returns result)

This ensures every workflow is executable via the hooks system.
