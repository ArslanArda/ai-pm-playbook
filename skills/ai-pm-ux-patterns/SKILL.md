---
name: ai-pm-ux-patterns
description: Use when the user is designing or reviewing the UX of an AI feature, including latency handling, confidence, fallbacks, human review, or AI-specific interaction patterns.
---

# AI PM UX Patterns

Use this skill for AI-specific user experience decisions.

## Read first

- `references/playbook/README.md`
- `references/playbook/SKILL.md`

Then load as needed:

- `references/playbook/frameworks/latency-ux.md`
- `references/playbook/frameworks/confidence-and-fallbacks.md`
- `references/playbook/frameworks/human-in-the-loop.md`
- `references/playbook/frameworks/conversational-vs-structured.md`
- `references/playbook/frameworks/error-and-hallucination-ux.md`
- `references/playbook/frameworks/personalization-ux.md`

Examples:

- `references/playbook/examples/ai-search-results-page.md`
- `references/playbook/examples/ai-onboarding-flow.md`
- `references/playbook/examples/ai-assisted-form.md`

## Working rules

- Design the low-confidence path as carefully as the happy path.
- Match interface style to task structure instead of defaulting to chat.
- Preserve user trust through clear fallback and correction paths.
