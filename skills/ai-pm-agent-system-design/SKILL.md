---
name: ai-pm-agent-system-design
description: Use when the user is deciding whether an AI workflow should be single-agent, multi-agent, routed, tool-using, or otherwise orchestrated as a product decision.
---

# AI PM Agent System Design

Use this skill when an AI workflow has become multi-step enough that architecture choices matter.

## Read first

- `references/playbook/README.md`
- `references/playbook/SKILL.md`

Then load as needed:

- `references/playbook/frameworks/single-vs-multi-agent.md`
- `references/playbook/frameworks/agent-pipeline-patterns.md`
- `references/playbook/frameworks/tool-and-mcp-design.md`
- `references/playbook/frameworks/guardrails-and-routing.md`
- `references/playbook/frameworks/token-cost-optimization.md`
- `references/playbook/frameworks/agent-observability.md`
- `references/playbook/frameworks/agent-failure-modes.md`

Examples:

- `references/playbook/examples/conversational-search-agent.md`
- `references/playbook/examples/content-generation-agent.md`
- `references/playbook/examples/support-copilot-agent.md`

## Working rules

- Start from the simplest viable architecture.
- Treat tool boundaries, fallback behavior, and observability as product decisions.
- Push back on “agentic” complexity if a bounded pipeline is enough.
