# Example: Evaluating Multi-Turn Context Management For Conversational Search

## Scenario

A property marketplace had a conversational search feature with a text-only message synthesizer.

The synthesizer did not emit structured filters directly. Instead, it took:

- prior conversation context
- the current active intent text
- the new user message

and produced one updated intent text for downstream search.

Examples:

- first turn: `Bakirkoy'de kiralik daire ariyoruz`
- later turn: `yeni binalari da getir`
- output: updated intent text that keeps the existing search and applies the new refinement

The team discovered that single-turn evals were not enough. The agent looked good when judged only on the latest message, but failed during real sessions by:

- dropping important earlier constraints
- carrying stale constraints too long
- mistaking a new search for a refinement
- adding narrowing language that hurt retrieval

## What Made Evaluation Tricky

This was not a normal `prompt -> answer` feature.

The real product job had two parts:

1. decide how the new user message relates to the existing search
2. produce the updated intent text for retrieval

That meant the team could not evaluate it well with:

- one gold string per example
- isolated last-turn prompts
- fluency-based scoring

Those methods missed the main product risk: wrong context management.

## The Eval Reframe

The PM reframed the unit of evaluation from:

- `new message -> synthesized query`

to:

- `previous intent text + new user message -> updated intent text`

and, for longer sessions:

- `conversation state at turn N + new user message -> updated state at turn N+1`

That change made the failure modes visible.

## What The Team Scored

The team used a three-layer evaluation strategy.

### Layer 1: Turn-Relation Accuracy

First, they scored whether the system understood what kind of update the user was making.

They labeled each turn as one of:

- `append`
- `refine`
- `broaden`
- `replace_partial`
- `reset_new_search`
- `meta_no_change`
- `ambiguous`

Example:

- previous intent: `Bakirkoy'de kiralik daireler`
- new message: `yeni binalari da getir`
- expected relation: `append`

Example:

- previous intent: `Bakirkoy'de kiralik daireler`
- new message: `vazgectim, Kadikoy'de satilik bakiyorum`
- expected relation: `reset_new_search`

### Layer 2: Updated-Intent Text Compliance

Because multiple updated texts could be acceptable, the team did not use exact-string matching.

Instead, each eval case included text obligations:

- `must_keep`
- `must_add`
- `may_add`
- `must_remove`
- `must_not_add`

This let the team judge whether the updated intent was faithful to the conversation while still allowing wording variation.

### Layer 3: Retrieval Impact

The team then checked whether the updated intent text actually improved search behavior downstream.

For each case they compared:

- raw new user message alone
- system-generated updated intent text
- human-written reference updated intent text

Then they reviewed:

- top-k relevance
- zero-result rate
- over-filtering rate
- obvious stale-carryover failures in returned inventory

## The Eval Case Template

Each benchmark row looked like this:

```md
### Case Metadata

- case_id:
- slice:
- priority:
- why_this_case_exists:

### Conversation State

- turn_history:
  - user:
  - assistant_or_system_intent:

- previous_intent_text:
- new_user_message:

### Expected Turn Relation

- expected_relation:
- relation_rationale:

### Text Expectations

- must_keep:
  -

- must_add:
  -

- may_add:
  -

- must_remove:
  -

- must_not_add:
  -

### Acceptable Outputs

- acceptable_output_1:
- acceptable_output_2:

### Bad Outputs

- bad_output_1:
  - why_bad:
- bad_output_2:
  - why_bad:

### Evaluation Notes

- retrieval_expectation:
- reviewer_notes:
```

## Example Benchmark Row

```md
### Case Metadata

- case_id: mtc_012
- slice: append_preference
- priority: high
- why_this_case_exists: checks whether the agent keeps earlier search context while adding a new building-age preference

### Conversation State

- turn_history:
  - user: Yasli annem icin Bakirkoy'de kiralik daire ariyoruz
  - assistant_or_system_intent: Bakirkoy'de kiralik, yasli birey icin uygun daireler

- previous_intent_text: Bakirkoy'de kiralik, yasli birey icin uygun daireler
- new_user_message: yeni binalari da getir

### Expected Turn Relation

- expected_relation: append
- relation_rationale: user is extending the same search rather than replacing it

### Text Expectations

- must_keep:
  - Bakirkoy
  - kiralik
  - daire
  - yasli birey ihtiyaci

- must_add:
  - yeni bina or yeni binalar

- may_add:
  - erisimi kolay
  - asansorlu

- must_remove:
  -

- must_not_add:
  - satilik
  - Istanbul geneli
  - 3+1
  - esyali

### Acceptable Outputs

- acceptable_output_1: Bakirkoy'de yasli birey icin uygun, yeni binalarda kiralik daireler
- acceptable_output_2: Bakirkoy'de kiralik daireler, yasli anne icin uygun ve yeni binalar

### Bad Outputs

- bad_output_1: Istanbul'da yeni binalarda kiralik daireler
  - why_bad: drops required prior location context

- bad_output_2: Bakirkoy'de satilik yeni daireler
  - why_bad: changes the search type instead of refining it

### Evaluation Notes

- retrieval_expectation: should keep Bakirkoy rental inventory and narrow toward newer buildings without collapsing recall
- reviewer_notes: if product policy explicitly maps elderly need to accessibility language, allow it only under may_add or must_add rules
```

## Core Metrics

The PM tracked a mix of turn-level and session-level metrics.

Turn-level:

- relation accuracy
- `must_keep` recall
- `must_add` recall
- `must_remove` precision
- `must_not_add` violation rate

State-management:

- dropped prior-context rate
- stale context carryover rate
- wrong reset rate
- harmful over-narrowing rate

Session-level:

- full-session pass rate
- first-error turn
- degradation after 3 or more turns

Retrieval:

- top-k judged relevance
- zero-result rate
- over-filtering rate

## Human Review Versus Grader Use

The team did not ask an LLM grader to judge “quality” broadly.

Instead:

- rules-based checks handled obvious keep, add, remove, and forbidden phrases
- human reviewers judged difficult ambiguity and policy-compliant operationalization
- an LLM grader was used only after calibration for criteria such as:
  - whether prior constraints were preserved
  - whether the new message was applied
  - whether stale context remained
  - whether the updated intent looked usable for search

## Launch Gates

The team used blocker-style metrics rather than one average score.

Example thresholds:

- dropped prior-context rate below `5%`
- stale context carryover below `3%`
- harmful over-narrowing below `2%`
- session pass rate above the chosen beta threshold
- no material regression in zero-result rate versus baseline

## Why This Worked

The key change was conceptual, not mathematical.

The PM stopped treating the feature as a query-rewriting problem and started treating it as a context-update problem.

That led to:

- better benchmark rows
- better error categories
- clearer launch blockers
- easier prompt and orchestration debugging

## Transferable Takeaway

If your AI feature updates an existing state, evaluate the update step directly.

Do not ask only, “Was the latest output good?”

Also ask:

- Did the system keep what should persist?
- Did it remove what should disappear?
- Did it understand whether the user was refining, replacing, or resetting?
- Did the updated output help the downstream system do the right thing?
