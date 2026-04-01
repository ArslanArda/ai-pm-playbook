# Example: Iterating A Search Intent Extraction Prompt

## Context

A property marketplace wanted to extract structured intent from natural-language queries in Turkish. The system needed to handle:

- ambiguous phrasing
- multi-intent requests
- common abbreviations and misspellings
- mixed hard and soft constraints

Output schema included:

- listing type
- budget
- location
- room count
- amenities
- ambiguity flag

## Version 1: Straight Extraction

The prompt simply asked the model to extract structured fields from the user query.

### Result

It worked well on clean, simple requests:

- “kadikoy 2+1 kiralik 35 bin”

It struggled on:

- multi-intent phrasing
- implicit buy vs. rent language
- colloquial district references

## Version 2: Add Ambiguity Rules

The prompt introduced explicit instructions:

- mark fields unknown when not clearly present
- set ambiguity flag if missing rent-vs-buy distinction or unclear price type
- do not guess district if multiple candidates fit

### Improvement

- fewer silent wrong assumptions
- clearer ambiguity handling

### New issue

- ambiguity flag became over-triggered on soft preferences, leading to too many clarification prompts downstream

## Version 3: Distinguish Retrieval-Critical Ambiguity From Soft Preference Ambiguity

The PM clarified product behavior:

- ambiguity flag should trigger only when uncertainty changes retrieval materially
- soft preferences like “quiet” or “family-friendly” should be extracted as soft signals, not blockers

### Improvement

- clarification rate dropped
- search flow became faster and less interruptive

### Remaining issue

- multi-intent queries like “kiralik ama uygunsa satilik da bakabilirim” still caused unstable extraction

## Version 4: Add Primary Intent Priority

The prompt added:

- when multiple intents exist, extract the primary actionable intent
- record secondary intent in notes field if schema allows
- if intents are equally weighted and materially different, set ambiguity flag

### Improvement

- multi-intent stability improved
- downstream search behavior became more consistent

### Remaining issue

- Turkish abbreviations and shorthand still caused misses on room count and district names

## Version 5: Add Language-Specific Guidance

The prompt explicitly referenced:

- common shorthand for room counts
- frequent district abbreviations
- tolerance for Turkish typos and agglutinative variation

### Improvement

- extraction accuracy rose on messy mobile queries
- less fallback to unknown fields on everyday shorthand

### Watchout

The team had to be careful not to overfit to a small shorthand list. Eval data was refreshed with new live-query examples monthly.

## What This Example Teaches

### 1. Good extraction prompts encode product logic, not just parsing logic

The crucial improvement was not “understand more Turkish.” It was “understand which ambiguity actually matters for retrieval.”

### 2. Multi-intent handling must reflect downstream product behavior

If the product cannot handle equal-weighted conflicting intents gracefully, the prompt should not pretend they can be collapsed cleanly.

### 3. Localization needs explicit attention

Language-specific quirks were not edge cases. They were mainstream behavior in the target market.
