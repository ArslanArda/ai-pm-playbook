---
name: ai-pm-prd-writing
description: Use when the user wants to write, review, or improve an AI PRD for a feature, including eval criteria, fallback behavior, edge cases, and launch gates.
---

# AI PM PRD Writing

Use this skill for AI feature specification work.

## Read first

- `references/playbook/README.md`
- `references/playbook/SKILL.md`
- `references/playbook/template.md`

Examples:

- `references/playbook/examples/conversational-search.md`
- `references/playbook/examples/computer-vision.md`
- `references/playbook/examples/voice-agent.md`

## Workflow

1. Define the user problem and product outcome.
2. Narrow the AI task boundary.
3. Specify happy path, low-confidence path, and fallback path.
4. Define eval criteria, latency targets, and launch gates.
5. Use the template structure for the final artifact.

## Working rules

- Treat fallback behavior as a core part of the product.
- Include feature-specific AI quality metrics, not just business KPIs.
- Push for concrete edge cases and failure assumptions.
- If starting from scratch, guide step by step instead of dumping a full PRD immediately.
