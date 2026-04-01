# Eval Data Strategy

Your eval set is not a one-time spreadsheet. It is a living product asset.

A weak eval dataset creates false confidence. A stale one creates drift blindness. An over-optimized one creates “teaching to the test,” where the system gets better at the eval rather than better for users.

## How To Bootstrap From Zero

Start with three buckets:

1. common real-world cases from logs or workflows
2. high-risk edge cases you know matter
3. adversarial or stress cases that reveal weak boundaries

Even a 50-100 example set can be useful early if coverage is thoughtful and tied to a clear rubric.

## How Many Examples Do You Need?

There is no universal number, but there is a useful rule:

- early exploration: enough examples to cover the main patterns and failure risks
- pre-launch: enough examples to detect meaningful regressions in the categories that matter most
- scaled production: enough volume and segmentation to catch drift by cohort, language, route, or feature type

The first goal is coverage, not brag-worthy dataset size.

## Versioning Principles

- keep dated dataset versions
- note additions, removals, and category changes
- separate benchmark sets from exploratory test sets
- record why each example exists if possible

This prevents quiet changes from destroying comparability.

## Avoiding “Teaching To The Test”

Common warning signs:

- prompt changes target benchmark quirks directly
- score rises, but user feedback does not
- the team knows the eval set too intimately
- failures keep appearing in production that the eval set never catches

Mitigations:

- refresh portions of the dataset regularly
- keep some holdout or surprise examples
- balance benchmark stability with new examples from recent failures

## Handling Edge Cases And Adversarial Inputs

Edge cases should not be random curiosities. Include them because they represent:

- common ambiguity
- known trust risks
- unsupported but likely user requests
- multilingual or localization challenges
- prompt injection or misuse attempts where relevant

## Realistic Use Scenarios

### Scenario 1: Conversational Search

The team starts with 80 examples: 40 common queries, 20 ambiguous queries, 10 unsupported requests, and 10 multilingual or typo-heavy cases. This is enough to compare prompt changes meaningfully early.

### Scenario 2: Content Generation

The team versions the eval set monthly by adding recent failure cases from production while keeping a core stable benchmark for regression checks.

## Questions To Ask Your Engineering Team

- Which real user scenarios are not represented in our current eval set?
- Do we know which examples are common, edge, or adversarial?
- How often should the eval set be refreshed without breaking comparability?
- Are we accidentally tuning too closely to a small benchmark?
- What recent production failures should be added as new cases?

## Anti-Patterns

### The Tiny Happy Benchmark

The eval set is small and mostly easy. What goes wrong: improvements look larger than they are.

### The Giant Uncurated Dump

The dataset is large but unlabeled and poorly segmented. What goes wrong: it becomes hard to interpret and maintain.

### The Frozen Benchmark

The team never updates the dataset after launch. What goes wrong: the eval slowly loses relevance as product and user behavior evolve.

## Red Flags

- No one knows where the eval examples came from
- The same examples are reused for every major decision without refresh
- Recent production failures are absent from the dataset
- Dataset size is discussed more than coverage quality
- Prompt improvements help the benchmark but not user outcomes

## Bottom Line

Build the smallest dataset that still covers the real decision surface, then version it like a product asset. Coverage, freshness, and comparability matter more than raw example count.
