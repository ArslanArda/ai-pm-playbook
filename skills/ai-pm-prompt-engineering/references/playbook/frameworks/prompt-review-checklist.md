# Prompt Review Checklist

Most prompt reviews are too shallow. The team looks at a few examples, likes the tone, and calls it done.

Use a structured review instead.

## Prompt Review Scorecard

| Area | Review question |
| --- | --- |
| Role clarity | Does the prompt define the assistant’s job clearly? |
| Constraint clarity | Are important “must not” instructions explicit? |
| Priority handling | If instructions conflict, is the priority obvious? |
| Format compliance | Is the output shape specified clearly enough for the UI? |
| Uncertainty behavior | Does the prompt say what to do when information is missing or confidence is low? |
| Grounding discipline | Does it prevent unsupported claims? |
| Example usefulness | Do examples teach the right pattern without overfitting? |

## Realistic Use Scenarios

### Scenario 1: Search Results Summary Prompt

Review reveals the prompt says “be helpful” more strongly than “do not infer unsupported neighborhood facts.” The likely result is polished overreach. The PM tightens constraint priority.

### Scenario 2: Support Draft Prompt

Review reveals the format section is vague about when to include escalation language. That creates UI inconsistency and agent confusion.

## Questions To Ask Your Engineering Team

- Which instruction currently carries the most product risk if misread?
- Are we relying on the model to infer output structure from examples instead of explicit rules?
- What happens when required context is missing?
- Does the prompt create any conflict between helpfulness and safety?
- Which review dimension is currently weakest in evals?

## Anti-Patterns

### Tone-Only Review

The team focuses on whether the output sounds good. What goes wrong: structural or safety failures slip through.

### Example Dependence

The prompt relies too heavily on examples instead of explicit instructions. What goes wrong: behavior becomes brittle outside shown patterns.

### Missing Low-Confidence Rule

The prompt says what to do when things are clear, but not when they are not. What goes wrong: confident guessing.

## Red Flags

- Important product rules appear only in examples
- Output formatting is inferred rather than stated
- There is no explicit instruction for unsupported requests
- Review conversations keep returning to “let’s see what happens”
- The prompt contains broad values but few enforceable constraints

## Bottom Line

Review prompts the way you review a risky feature spec: clarity, constraints, failure behavior, and downstream compatibility matter more than elegant phrasing.
