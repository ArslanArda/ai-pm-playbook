# Prompt Engineering For PMs

Prompt engineering is often treated as an implementation detail. For product work, that is a mistake.

In many AI features, the prompt is not just a technical instruction. It is the behavior definition of the product:

- what the assistant is allowed to do
- how it should respond
- what it must avoid
- what format it should produce
- how it behaves under ambiguity

Changing the prompt can change the user experience as materially as changing a UI flow or business rule. That is why PMs should care about prompt design, review, versioning, and debugging even when engineers own the implementation mechanics.

This section is about prompt engineering from that PM perspective.

## What This Section Covers

- [`SKILL.md`](./SKILL.md): guided workflow for specifying and improving prompts as product behavior
- [`frameworks/prompt-as-product-spec.md`](./frameworks/prompt-as-product-spec.md): why prompts should be treated like product specs
- [`frameworks/versioning-and-testing.md`](./frameworks/versioning-and-testing.md): how to version, test, and roll back prompt changes
- [`frameworks/prompt-review-checklist.md`](./frameworks/prompt-review-checklist.md): a systematic way to review prompts before shipping
- [`frameworks/system-prompt-design.md`](./frameworks/system-prompt-design.md): the anatomy of a production system prompt
- [`frameworks/prompt-debugging.md`](./frameworks/prompt-debugging.md): how to figure out whether bad output is a prompt problem, model problem, or data problem
- [`examples/listing-description-agent.md`](./examples/listing-description-agent.md)
- [`examples/search-intent-extraction.md`](./examples/search-intent-extraction.md)
- [`examples/content-grader-prompt.md`](./examples/content-grader-prompt.md)

## Opinionated Recommendations

### Recommendation 1: PMs should own prompt intent, not just review output samples

The PM should define desired behavior, guardrails, and tradeoffs. Engineers should operationalize that behavior reliably.

### Recommendation 2: Prompt changes deserve the same discipline as feature changes

Version prompts, test them on eval sets, and note regressions. Do not treat them like invisible copy edits.

### Recommendation 3: Most prompt failures are not “the model being weird”

They are often one of:

- ambiguous instructions
- conflicting priorities
- weak context
- missing format constraints
- scope that the prompt was never designed to handle

### Recommendation 4: Debug by isolating variables

If you change prompt, model, context, and routing all at once, you learn very little.

## The PM Lens

Prompt work becomes much better when you ask product questions:

- What exact behavior should the system show here?
- Which failure is most harmful?
- Which instructions are mandatory versus nice to have?
- What should happen when context is missing?
- What user-facing format is required by the product surface?

That moves prompt engineering from “wordsmithing” to behavior design.
