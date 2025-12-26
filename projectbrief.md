# Project Brief: n8n Workflow Generation Agent

## Overview

An intelligent automation system that simplifies n8n workflow creation by leveraging Claude Code as the core AI agent, enhanced with specialized n8n skills for expert-level workflow generation.

## Problem Statement

Creating n8n workflows programmatically presents several challenges for users:

- Steep learning curve for n8n's node configuration and expression syntax
- Complex validation requirements and cryptic error messages
- Difficulty selecting appropriate workflow patterns for specific use cases
- Time-consuming trial-and-error when configuring node dependencies

## Solution

A conversational AI agent powered by Claude Code that transforms natural language descriptions into production-ready n8n workflows. The agent utilizes the n8n-skills package to provide expert knowledge across seven domains: expression syntax, MCP tools, workflow patterns, validation, node configuration, JavaScript code nodes, and Python code nodes.

## Core Components

**AI Agent (Claude Code)**: The reasoning engine that interprets user requests, designs workflow architecture, and generates valid workflow JSON.

**n8n-mcp Server**: Model Context Protocol server providing real-time access to 525+ n8n nodes, 2,653+ workflow templates, and comprehensive validation tools.

**n8n Skills Package**: Seven complementary skills that activate contextually to guide the agent through expression syntax, tool usage, pattern selection, validation, and node configuration.

## User Experience

A user describes their automation goal in plain language. The agent analyzes the request, selects an appropriate workflow pattern, identifies required nodes, configures each node with correct parameters, validates the complete workflow, and delivers an importable JSON file ready for n8n.

Example interaction:

> **User**: "When a new row is added to my Google Sheet, send a Slack notification to the #updates channel with the row data."
>
> **Agent**: Generates a validated workflow with Google Sheets trigger → Slack message node, properly configured with expressions for data mapping.

## Technical Architecture

```
┌─────────────────────────────────────────────────────────┐
│                      User Request                        │
└─────────────────────────────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────┐
│                     Claude Code Agent                    │
│  ┌─────────────────────────────────────────────────┐    │
│  │              n8n Skills (7 domains)              │    │
│  │  • Expression Syntax    • Validation Expert     │    │
│  │  • MCP Tools Expert     • Node Configuration    │    │
│  │  • Workflow Patterns    • Code JS/Python        │    │
│  └─────────────────────────────────────────────────┘    │
└─────────────────────────────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────┐
│                     n8n-mcp Server                       │
│  • Node search & discovery (525+ nodes)                 │
│  • Template library (2,653+ workflows)                  │
│  • Workflow validation                                  │
│  • Node configuration schemas                           │
└─────────────────────────────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────┐
│              Validated n8n Workflow JSON                 │
└─────────────────────────────────────────────────────────┘
```

## Key Capabilities

**Intelligent Pattern Selection**: Automatically identifies the best workflow pattern (webhook processing, HTTP API integration, database operations, AI workflows, or scheduled tasks) based on the user's requirements.

**Validation-First Approach**: Every generated workflow passes through comprehensive validation before delivery, catching configuration errors, expression syntax issues, and connection problems.

**Context-Aware Configuration**: Understands node dependencies and property visibility rules, ensuring that configurations like `sendBody=true` correctly reveal related body parameters.

**Error Recovery**: When validation fails, the agent interprets errors, applies fixes, and re-validates until the workflow is production-ready.

## Success Metrics

- Workflow generation accuracy: Target 95%+ first-attempt validation pass rate
- User satisfaction: Workflows require minimal manual adjustment after generation
- Coverage: Support for common automation patterns across 100+ popular integrations

## Dependencies

- Claude Code with MCP support
- n8n-mcp server (installed and configured)
- n8n-skills package (7 skills installed)
- n8n instance for workflow deployment

## Project Scope

**In Scope**: Workflow generation from natural language, node configuration, expression writing, validation, and JSON export.

**Out of Scope**: Direct n8n instance management, credential setup, workflow execution monitoring, and custom node development.

## Timeline Estimate

- Phase 1 (Setup): n8n-mcp server and skills installation — 1 day
- Phase 2 (Integration): Agent configuration and testing — 2-3 days  
- Phase 3 (Refinement): Prompt optimization and edge case handling — 1 week

---

*This system transforms the complexity of n8n workflow creation into a simple conversation, making automation accessible to users regardless of their technical expertise with n8n.*