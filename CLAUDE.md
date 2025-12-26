# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is an n8n workflow generation agent that transforms natural language descriptions into production-ready n8n workflows. The system uses Claude Code as the AI agent, enhanced with n8n-mcp server and n8n-skills package.

## Architecture

```
User Request → Claude Code Agent (with 7 n8n skills) → n8n-mcp Server → Validated Workflow JSON
```

**Key Components:**
- **Claude Code Agent**: Interprets requests, designs workflow architecture, generates valid workflow JSON
- **n8n-mcp Server**: Provides access to 525+ nodes, 2,653+ templates, and validation tools
- **n8n Skills**: Seven domain-specific skills (expression syntax, MCP tools, workflow patterns, validation, node configuration, JS code nodes, Python code nodes)

## Available n8n Skills

The following skills are installed and available for use:
- `n8n-expression-syntax` - Validate expressions and fix common errors
- `n8n-mcp-tools-expert` - Guide for using n8n-mcp tools effectively
- `n8n-workflow-patterns` - Proven architectural patterns from real workflows
- `n8n-validation-expert` - Interpret validation errors and guide fixes
- `n8n-node-configuration` - Operation-aware node configuration guidance
- `n8n-code-javascript` - Write JavaScript in n8n Code nodes
- `n8n-code-python` - Write Python in n8n Code nodes

## Dependencies

- Claude Code with MCP support
- n8n-mcp server (configured)
- n8n instance for workflow deployment

## Workflow Generation Approach

1. Analyze user's natural language request
2. Select appropriate workflow pattern (webhook processing, HTTP API integration, database operations, AI workflows, or scheduled tasks)
3. Identify required n8n nodes
4. Configure each node with correct parameters and expressions
5. Validate the complete workflow
6. Deliver importable JSON file

## Key Constraints

- **Validation-first**: All generated workflows must pass validation before delivery
- **Context-aware configuration**: Node dependencies and property visibility rules matter (e.g., `sendBody=true` must reveal body parameters)
- **Error recovery**: When validation fails, interpret errors, apply fixes, re-validate

## Scope Boundaries

**In scope**: Workflow generation, node configuration, expression writing, validation, JSON export

**Out of scope**: n8n instance management, credential setup, workflow execution monitoring, custom node development
