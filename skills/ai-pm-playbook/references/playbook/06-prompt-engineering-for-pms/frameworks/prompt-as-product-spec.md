# Prompt As Product Spec

If the prompt determines what the AI is allowed to infer, when it should ask a follow-up, how it should refuse, and what it must return to the UI, then the prompt is not implementation dust. It is a product spec written in a model-readable format.

Treat it that way.

## The Default

Write a prompt spec before prompt implementation whenever the AI behavior will:

- touch user-facing copy
- drive downstream workflow logic
- enforce policy or safety boundaries
- influence launch-readiness decisions
- require explicit fallback behavior

Do not wait for prompt behavior to become unstable before creating the spec. That is too late.

## Prompt Spec Template

Use this template as a real artifact, not as a checklist you skim once.

| Spec element | What PM should define | Why it matters |
| --- | --- | --- |
| Feature name | The exact feature or subflow this prompt serves | Prevents one prompt from silently expanding into multiple jobs |
| User moment | Where in the workflow the user encounters this behavior | Keeps the prompt anchored to product context |
| Primary job | The one job the prompt must do well | Prevents scope creep |
| Non-goals | What this prompt will not do | Gives the team permission to say no |
| Inputs available | What context, structured fields, and metadata the model receives | Avoids designing behavior the system cannot support |
| Allowed inferences | What the model may infer when evidence is partial | Prevents over-helpful guessing |
| Forbidden claims | Facts or decisions the model must never invent or overstate | Protects trust and compliance |
| Confidence behavior | What to do when evidence is weak or ambiguous | Defines the user experience of uncertainty |
| Escalation or fallback path | What happens when the prompt cannot complete the job safely | Prevents dead-end failure states |
| Output contract | Exact schema, tone limits, or UI formatting requirements | Keeps downstream surfaces stable |
| Evaluation slices | Which scenarios must be measured before launch | Prevents average-quality blindness |
| Launch blockers | Which failure types block rollout even if headline quality looks fine | Creates a real go / no-go gate |

## Working Prompt Spec Example

### Example: Search Intent Extraction For Property Search

| Spec element | Example definition |
| --- | --- |
| Feature name | Conversational property search intent extraction |
| User moment | User enters a natural-language query before results retrieval |
| Primary job | Convert the user request into structured search intent without silently dropping material constraints |
| Non-goals | Do not answer neighborhood quality questions, do not rank results, do not estimate price fairness |
| Inputs available | Raw user query, locale, recent refinement chips, session language |
| Allowed inferences | Normalize room-count shorthand, infer listing type only when explicitly stated or strongly implied by local phrasing patterns |
| Forbidden claims | Do not guess district, budget currency, or amenity presence if not grounded in the query |
| Confidence behavior | Ask for clarification only when ambiguity changes retrieval materially; otherwise mark soft preferences separately |
| Escalation or fallback path | If intent remains materially ambiguous after one clarification, show standard structured filters instead of continuing chat-only refinement |
| Output contract | JSON with `listing_type`, `budget_min`, `budget_max`, `location`, `room_count`, `amenities`, `soft_preferences`, `ambiguity_flag`, `notes` |
| Evaluation slices | typo-heavy Turkish queries, multi-intent phrasing, colloquial district references, mixed hard and soft constraints |
| Launch blockers | silent constraint-drop rate above `5%`; incorrect listing-type inference above `3%`; clarification prompt rate above `18%` |

That table is already more useful than a vague prompt request like "make search understand messy Turkish better."

## What Belongs In The Spec Versus The Prompt

### Put it in the spec

- product goal
- scope boundaries
- non-goals
- risk tolerance
- launch blockers
- user-facing fallback behavior

### Put it in the prompt

- task framing
- behavioral rules
- output schema
- uncertainty instructions
- examples that teach edge patterns

### Put it outside both

- deterministic validation
- analytics instrumentation
- rollout rules
- UI state transitions

This boundary matters. Weak teams stuff everything into the prompt because it is the fastest place to edit.

## Realistic Use Scenarios

### Scenario 1: Search Explanation Prompt

The PM must define whether the assistant may:

- infer qualitative neighborhood traits
- collapse several reasons into one summary
- mention uncertainty explicitly
- cite listing facts versus broader market facts

Those are product-policy decisions. The prompt implementation comes later.

### Scenario 2: Support Drafting Prompt

The PM must define:

- whether the AI can suggest account credits
- whether it may cite policy exceptions
- when the draft must force human review
- what refusal or escalation language is acceptable

If you skip the spec, the team ends up debating those rules inside prompt text reviews.

## Questions To Ask Your Engineering Team

- Which behaviors in the current prompt would surprise a PM if they were written plainly in a product doc?
- Which prompt rules are compensating for missing system constraints or weak UI design?
- Which failure types should block launch even if average output quality improves?
- If we changed this prompt today, what downstream system or UI assumptions might break?
- Which behaviors are hidden in few-shot examples instead of explicit rules?

## Anti-Patterns

### Prompt As Hidden Policy

What happens:

- product rules live only in the system prompt
- PM review focuses on outputs, not contract

Why it happens:

- prompt editing is faster than writing the policy down

What to do instead:

- require a prompt spec artifact for any user-facing behavior or policy-sensitive flow

### Prompt As Wish List

What happens:

- the prompt asks for helpfulness, accuracy, empathy, brevity, conversion, and caution all at once

Why it happens:

- nobody forced priority tradeoffs

What to do instead:

- rank the top two priorities and explicitly state what loses when they conflict

### Prompt Without Non-Goals

What happens:

- the model expands into adjacent tasks

Why it happens:

- PMs define the happy path but not the boundary

What to do instead:

- write non-goals directly into the prompt spec and treat them as reviewable

## Red Flags

- No product artifact describes prompt behavior in plain language
- Prompt changes ship without updated launch blockers or eval slices
- The team cannot name which behaviors are allowed inferences versus forbidden guesses
- UI components depend on output structure the prompt only "usually" follows
- Prompt review meetings focus on tone more than behavior risk

## Bottom Line

The prompt spec is the PM's way of making AI behavior legible before it becomes code, copy, or production risk. If the team skips that step, prompt work becomes fast but fragile.
