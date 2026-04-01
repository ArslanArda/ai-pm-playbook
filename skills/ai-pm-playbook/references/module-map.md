# Module Map

Use these bundled modules as needed.

These are modules inside one skill, not separate skills. Route across them when the user’s problem crosses boundaries.

## Core Modules

- `references/playbook/01-ai-prd-writing/`
  Use for feature definition, launch gates, fallback behavior, and edge cases.

- `references/playbook/02-evaluation-design/`
  Use for rubrics, eval sets, graders, and error analysis.

- `references/playbook/03-model-strategy/`
  Use for prompt-first vs buy vs custom, routing, and cost-latency-quality tradeoffs.

- `references/playbook/04-ai-agent-system-design/`
  Use for single vs multi-agent decisions, tools, guardrails, and observability.

- `references/playbook/05-ai-team-operations/`
  Use for mission cadence, DACI, review rituals, adoption, and stakeholder communication.

- `references/playbook/06-prompt-engineering-for-pms/`
  Use for prompt specification, review, testing, versioning, and debugging.

- `references/playbook/07-ai-ux-patterns/`
  Use for latency UX, confidence handling, control, fallback design, and personalization.

## Typical Cross-Module Combinations

- New AI feature:
  PRD writing + evaluation design + AI UX

- Complex AI workflow:
  PRD writing + model strategy + agent system design + evaluation design

- Unstable output quality:
  evaluation design + prompt engineering + model strategy

- Launch planning:
  PRD writing + evaluation design + team operations + AI UX
