# Prompt As Product Spec

For many AI features, the prompt is the closest thing you have to a behavior contract.

If the system prompt says:

- how to interpret user requests
- what to prioritize
- what to refuse
- what format to produce

then prompt changes are effectively product changes.

## Prompt Spec Template

| Spec element | What PM should define |
| --- | --- |
| Job to be done | What exact task the prompt serves |
| User value | Why this behavior matters |
| Allowed behavior | What the assistant should do |
| Forbidden behavior | What it must never do |
| Fallback behavior | What happens under uncertainty |
| Output format | How the response must look |
| Review method | How quality will be checked |

## Realistic Use Scenarios

### Scenario 1: Search Explanation Prompt

The prompt is not just “write a helpful summary.” It defines whether the assistant can infer neighborhood traits, how to talk about uncertainty, and how much explanation is shown before results. That is product behavior.

### Scenario 2: Support Drafting Prompt

The prompt defines whether the assistant can suggest policy exceptions, how apologetic the tone should be, and when to escalate. That is not copy polish. It is policy-facing product behavior.

## Questions To Ask Your Engineering Team

- Which product behaviors are currently encoded only in prompts?
- Which prompt sections correspond to user-facing rules or policy decisions?
- What changes in the UI or workflow if we change this prompt?
- Which behaviors deserve explicit product approval before prompt edits ship?
- Are prompt changes being tracked like feature changes or like hidden config edits?

## Anti-Patterns

### Prompt As Implementation Dust

Teams treat the prompt as an engineering detail. What goes wrong: PM ownership of behavior becomes weak.

### Prompt As Wish List

The prompt contains desired behavior but not explicit constraints. What goes wrong: the model optimizes for fluency rather than product intent.

### Prompt Without Non-Goals

The prompt defines what to do but not what not to do. What goes wrong: scope drift and unsafe helpfulness.

## Red Flags

- No product artifact describes prompt behavior clearly
- Prompt changes reach production without PM review
- The UI expects structured behavior the prompt does not explicitly demand
- Teams cannot explain why the prompt says what it says
- Guardrails live only outside the prompt, with no behavioral alignment

## Bottom Line

Treat prompts like product specs for AI behavior. If the prompt changes the user experience, it deserves product clarity, review, and version discipline.
