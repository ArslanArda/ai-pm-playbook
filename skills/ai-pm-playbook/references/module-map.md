# Module Map

Use these bundled modules as needed.

These are modules inside one skill, not separate skills. The skill is agent-centered, so start from agent system design unless the task is clearly anchored elsewhere. Route across modules when the user’s problem crosses boundaries.

## Default Starting Point

- `references/playbook/04-ai-agent-system-design/`
  Use first for orchestration choices, tool boundaries, single-vs-multi-agent decisions, agent instruction packs, guardrails, observability, and cost-latency tradeoffs.

## Context Intake

- `references/playbook/my-product/qa-reference.md`
  Use when product context is missing, stale, or too thin to support a serious recommendation.

## Supporting Modules

- `references/playbook/01-ai-prd-writing/`
  Use when the agent design needs sharper task boundaries, fallback behavior, human review rules, launch gates, or edge cases.

- `references/playbook/02-evaluation-design/`
  Use for rubrics, eval sets, graders, launch thresholds, and error analysis.

- `references/playbook/03-model-strategy/`
  Use for prompt-first vs buy vs custom, routing, and cost-latency-quality tradeoffs.

- `references/playbook/05-ai-team-operations/`
  Use for mission cadence, DACI, review rituals, adoption, and stakeholder communication.

- `references/playbook/06-prompt-engineering-for-pms/`
  Use for prompt specification, review, testing, versioning, and debugging.

- `references/playbook/07-ai-ux-patterns/`
  Use for latency UX, confidence handling, control, fallback design, and personalization.

## Typical Cross-Module Combinations

- New agentic feature:
  agent system design + PRD writing + evaluation design + AI UX

- Agent instruction request:
  agent system design + prompt engineering + evaluation design

- Tool-using workflow:
  agent system design + model strategy + evaluation design

- Unstable output quality:
  agent system design + evaluation design + prompt engineering + model strategy

- Launch planning for an agent:
  PRD writing + evaluation design + team operations + AI UX + agent system design
