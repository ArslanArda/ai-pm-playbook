---
name: ai-pm-model-strategy
description: Use when the user needs a product-facing recommendation on model choice, routing, or build-vs-buy-vs-prompt tradeoffs for an AI feature.
---

# AI PM Model Strategy

Use this skill for model selection and tradeoff work from a PM perspective.

## Read first

- `references/playbook/README.md`
- `references/playbook/SKILL.md`

Then load as needed:

- `references/playbook/frameworks/build-vs-buy-vs-prompt.md`
- `references/playbook/frameworks/model-routing.md`
- `references/playbook/frameworks/cost-latency-quality.md`

## Workflow

1. Define the exact task the model must do.
2. Set the quality bar, latency ceiling, and cost sensitivity.
3. Evaluate whether prompt-first is enough.
4. Recommend prompt-only, external capability, routing, or custom adaptation.
5. Make fallback logic and tradeoffs explicit.

## Working rules

- Keep the conversation anchored in product needs, not model names.
- Challenge routing unless request tiers are real and measurable.
- Explain cost, latency, and quality tradeoffs directly.
