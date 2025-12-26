# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is an n8n workflow generation agent that transforms natural language descriptions into production-ready n8n workflows. The system uses Claude Code as the AI agent with n8n skills for workflow design.

## Architecture

```
User Request → Claude Code Agent (with n8n skills) → Generates:
                                                     ├── workflows/   (JSON)
                                                     ├── prompts/     (AI node prompts)
                                                     ├── code/        (Code node scripts)
                                                     └── hooks/       (trigger scripts)
                                                            ↓
                                                     User runs hook
                                                            ↓
                                                     Webhook → n8n Workflow → Webhook Response
```

## Folder Structure

- `workflows/` - n8n workflow JSON files (importable directly to n8n)
- `prompts/` - System prompts for AI Agent nodes (copy into n8n)
- `code/javascript/` - JavaScript code for Code nodes
- `code/python/` - Python code for Code nodes
- `hooks/` - Shell scripts to trigger workflows via webhook

## Available n8n Skills

The following skills are installed and available for use:
- `n8n-expression-syntax` - Validate expressions and fix common errors
- `n8n-workflow-patterns` - Proven architectural patterns from real workflows
- `n8n-validation-expert` - Interpret validation errors and guide fixes
- `n8n-node-configuration` - Operation-aware node configuration guidance
- `n8n-code-javascript` - Write JavaScript in n8n Code nodes
- `n8n-code-python` - Write Python in n8n Code nodes

## Workflow Generation Rules

### Webhook Pattern (Required)
All workflows MUST follow this pattern:
1. **Start**: Webhook node (trigger)
2. **Middle**: Processing nodes
3. **End**: Webhook Response node (returns result)

### Output Separation
To minimize token usage, separate heavy content from workflow JSON:
- **System prompts**: Write to `prompts/<workflow-name>.md`
- **Code snippets**: Write to `code/javascript/<name>.js` or `code/python/<name>.py`
- **Workflow JSON**: Reference prompts/code by placeholder, user copies content manually

### Hook Scripts
For each workflow, create a corresponding hook script in `hooks/`:
```bash
#!/bin/bash
curl -X POST "http://localhost:5678/webhook/<path>" \
  -H "Content-Type: application/json" \
  -d '{"input": "value"}'
```

## Workflow Generation Approach

1. Analyze user's natural language request
2. Design webhook-based workflow architecture
3. Identify required n8n nodes
4. Generate workflow JSON (with placeholder references for prompts/code)
5. Write system prompts to `prompts/`
6. Write code snippets to `code/`
7. Create hook script in `hooks/`

## Key Constraints

- **Webhook-first**: All workflows start with Webhook, end with Webhook Response
- **Separation of concerns**: Heavy content (prompts, code) stored separately from workflow JSON
- **Runnable hooks**: Each workflow has a corresponding trigger script

## Scope Boundaries

**In scope**: Workflow generation, prompt writing, code generation, hook scripts, JSON export

**Out of scope**: n8n instance management, credential setup, workflow execution monitoring, custom node development
