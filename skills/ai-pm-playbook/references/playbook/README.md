# AI PM Playbook Overview

This bundled overview exists to orient the skill, not to teach a GitHub workflow.

Use it when you need a compact map of what the playbook covers and how the modules fit together.

## What This Playbook Is

The AI PM Playbook is a practical operating system for product managers building AI-native products. It is designed for real product work where ambiguity, latency, cost, evaluation quality, user trust, and organizational friction all matter at the same time.

This is not an engineering skill and it is not a vendor-selection guide. The focus is product definition, evaluation, model decisions, agent-system choices, prompt behavior, AI UX, and operating cadence.

## What The Skill Should Do With It

Use the playbook to help the user:

- define the right artifact or decision
- pressure-test product assumptions
- connect choices across PRD, eval, model, prompt, orchestration, UX, and rollout
- produce reusable PM outputs instead of generic commentary

Do not answer by telling the user to browse the playbook unless they explicitly ask to inspect source material.

## Core Modules

| Module | What it covers |
| --- | --- |
| [`00-how-to-use`](./00-how-to-use/README.md) | How to run the playbook as a working method rather than static reading |
| [`01-ai-prd-writing`](./01-ai-prd-writing/README.md) | AI PRDs with behavior definition, evals, fallback logic, and failure handling |
| [`02-evaluation-design`](./02-evaluation-design/README.md) | Eval plans, graders, datasets, error analysis, and quality review structure |
| [`03-model-strategy`](./03-model-strategy/README.md) | Model selection, routing, and cost-latency-quality tradeoffs |
| [`04-ai-agent-system-design`](./04-ai-agent-system-design/README.md) | Agent architecture, tools, guardrails, failure modes, and observability |
| [`05-ai-team-operations`](./05-ai-team-operations/README.md) | Mission cadence, DACI, rituals, adoption, and stakeholder communication |
| [`06-prompt-engineering-for-pms`](./06-prompt-engineering-for-pms/README.md) | Prompt specification, versioning, testing, review, and debugging |
| [`07-ai-ux-patterns`](./07-ai-ux-patterns/README.md) | Latency UX, confidence handling, fallbacks, conversational patterns, and personalization |
| [`appendix`](./appendix/glossary.md) | Glossary, reading list, and tool landscape |

## Default Operating Pattern

1. Read local product context first.
2. Choose the module closest to the current bottleneck.
3. Pull in one or two adjacent modules when the task clearly spans them.
4. Use the relevant `SKILL.md`, template, framework, or example to sharpen the output.
5. Produce a concrete deliverable, recommendation, or review, then pressure-test it.

## When To Combine Modules

- New AI feature: PRD writing + evaluation design + AI UX
- Routing or model debate: model strategy + evaluation design + prompt engineering
- Agent workflow design: agent system design + model strategy + evaluation design
- Launch readiness review: PRD writing + evaluation design + AI UX + team operations

## Product Context

The preferred product context source is `my-product/PRODUCT_CONTEXT.md` in the current workspace.

If that file is missing, use [`my-product/PRODUCT_CONTEXT.template.md`](./my-product/PRODUCT_CONTEXT.template.md) to define the missing context before making high-confidence recommendations.
