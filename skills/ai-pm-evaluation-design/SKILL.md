---
name: ai-pm-evaluation-design
description: Use when the user needs to design evaluation criteria, datasets, grader workflows, or error analysis for an AI feature.
---

# AI PM Evaluation Design

Use this skill for launch gates, eval planning, grader design, and failure analysis.

## Read first

- `references/playbook/README.md`
- `references/playbook/SKILL.md`

Then load as needed:

- `references/playbook/frameworks/grader-agent-pattern.md`
- `references/playbook/frameworks/error-analysis.md`
- `references/playbook/frameworks/eval-data-strategy.md`

## Workflow

1. Define the quality rubric first.
2. Separate deterministic checks, human review, and graders.
3. Build or refine the eval set with common, edge, and adversarial cases.
4. Analyze failures by category, not just average score.
5. Convert the eval output into launch or prioritization decisions.

## Working rules

- Do not accept vague quality definitions.
- If a grader is involved, test grader-vs-human agreement.
- Prioritize blocker failure categories over flattering aggregate metrics.
