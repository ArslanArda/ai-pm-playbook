# System Prompt Design

A production system prompt should look like a behavior contract, not a brainstorm.

The PM concern is not literary quality. It is whether the prompt makes the product's behavior stable, reviewable, and measurable.

## Core Anatomy

| Component | What it should do | Product impact if missing |
| --- | --- | --- |
| Role / job definition | State the exact job the assistant is performing in this flow | The model drifts into adjacent tasks |
| Decision priorities | Define what matters most when tradeoffs appear | Behavior changes unpredictably across edge cases |
| Behavioral constraints | State what the model must never do | Over-helpful or unsafe behavior slips through |
| Allowed inputs and evidence rules | Clarify what sources count as valid grounding | Wrong claims sound polished |
| Output format | Specify the exact return shape the UI or workflow needs | Downstream systems become brittle |
| Fallback or refusal rules | Define behavior under uncertainty or unsupported scope | Users get confident nonsense or dead-end failure |
| Few-shot examples | Teach the model edge patterns the rules alone do not capture | Edge-case execution stays unstable |
| Reasoning or effort guidance | Shape how much work the model should do before answering | Latency and verbosity drift |

## Recommended Prompt Structure

Use a consistent order. Do not improvise structure every sprint.

1. Job definition
2. Decision priorities
3. Non-goals and forbidden behavior
4. Grounding or evidence rules
5. Output schema
6. Fallback or refusal behavior
7. Few-shot examples
8. Final reminder for the highest-risk rule

That order forces the important rules to appear before the examples and formatting detail.

## Bad Prompt Structure Versus Better Prompt Structure

### Bad

```text
You are a very helpful AI assistant for real estate users. Be friendly, concise, informative,
and persuasive. Help users find what they want. Output structured data when possible. Avoid mistakes.
If the user is unclear, ask follow-up questions. You know Turkish property search really well.
```

Problems:

- no explicit product job
- no boundary on allowed inference
- no output contract
- no rule for when to ask versus act
- no grounding standard

### Better

```text
You extract search intent for a property marketplace before retrieval.

Priority order:
1. Do not drop material user constraints.
2. Do not guess fields that change retrieval materially.
3. Prefer one-pass extraction over clarification unless ambiguity changes retrieval.

You may normalize room-count shorthand and common location abbreviations.
You must not invent district, budget, or amenity fields when evidence is absent.

Return valid JSON with:
- listing_type
- location
- budget_min
- budget_max
- room_count
- amenities
- soft_preferences
- ambiguity_flag
- notes

If retrieval-critical ambiguity remains, set ambiguity_flag=true and include one short clarification question in notes.
```

This version is not prettier. It is simply legible and enforceable.

## Token Budget Discipline

When prompts get too long, most teams cut the wrong things.

### Cut in this order

1. Redundant tone language
2. Repeated formatting reminders
3. Examples that teach the same pattern twice
4. Long policy prose that should be rewritten as short rules

### Protect in this order

1. The primary job definition
2. The highest-risk constraint
3. The output contract
4. The fallback rule

If the prompt is over budget and your first instinct is to cut the fallback rule, you are cutting the wrong part.

## What Belongs In Prompt Versus Validation

### Belongs in prompt

- how to interpret the task
- which priorities win on conflict
- what kinds of inference are allowed
- how to express uncertainty
- what output shape to produce

### Belongs in deterministic validation or orchestration

- schema enforcement
- retry logic
- hard business-rule checks
- routing to different downstream actions
- audit logging

Do not tell the prompt to "always return valid JSON" and pretend that replaces validation.

## Realistic Use Scenarios

### Scenario 1: Listing Description Agent

Without explicit grounding constraints, the model will often write copy that sounds more marketable than the source listing. The short-term output looks better. The long-term result is trust damage and complaints from agents whose listings were embellished.

### Scenario 2: Search Intent Extractor

Without a strict output contract, extraction quality can be acceptable while the feature still feels flaky because the downstream search system receives inconsistent keys, missing booleans, or mixed free text.

## Questions To Ask Your Engineering Team

- Which prompt section is carrying a product decision that should be visible in a PRD or spec?
- Which rules are repeated because the prompt structure is weak?
- Which few-shot examples are masking unclear instructions?
- If we had to save 20 percent of prompt tokens today, what would we cut first and why?
- Which fallback rules should stay in prompt and which should become deterministic validation?

## Anti-Patterns

### Persona Overload

What happens:

- half the prompt is about tone, helpfulness, and brand personality

Why it happens:

- persona feels easier to write than behavioral rules

What to do instead:

- keep tone short and spend the tokens on product-critical behavior

### Format By Hope

What happens:

- the UI expects structured output, but the prompt only suggests it

Why it happens:

- the team assumes the model will infer the desired schema

What to do instead:

- specify fields, types, and fallback values explicitly

### Constraint Burial

What happens:

- the most important rule appears once in the middle of a long paragraph

Why it happens:

- prompt authors optimize for "natural writing" over rule clarity

What to do instead:

- isolate the top-risk rule and restate it near the end

## Red Flags

- The prompt is one long paragraph
- The output structure is only partially specified
- Few-shot examples contradict explicit rules
- The team cannot say which prompt section most affects latency
- The fallback behavior changes from one release to the next without a product decision

## Bottom Line

A good system prompt is not poetic. It is structured enough that a PM, engineer, and reviewer can all explain what the model is supposed to do and what should happen when it cannot do it well.
