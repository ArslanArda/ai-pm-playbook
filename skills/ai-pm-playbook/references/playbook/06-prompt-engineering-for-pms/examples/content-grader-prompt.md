# Example: Refining A Content Grader Prompt Through Human Disagreement Analysis

## Context

A team used an LLM grader to score AI-generated listing descriptions. The grader had to evaluate:

- groundedness
- specificity
- readability
- policy compliance

Human reviewers checked a sample set weekly.

## Initial Grader Prompt

The first grader prompt asked:

- whether the description was high quality
- whether it was helpful
- whether it should pass

### What happened

- grader scores were broadly positive
- humans still rejected a meaningful share of outputs
- disagreement was highest on generic filler and subtle unsupported claims

The grader liked polished text too much.

## First Refinement: Replace Vague Criteria With Explicit Rules

The prompt was changed to ask:

- does the text mention only facts present in the input?
- does it include at least two concrete listing details?
- does it avoid unsupported neighborhood or amenity claims?
- does it avoid generic filler phrases?

### Improvement

- grader-human agreement improved materially on grounding
- pass/fail became easier to interpret

### Remaining issue

- grader still passed some descriptions humans found weak because they were technically correct but too bland

## Second Refinement: Add Negative Anchors

The PM and content ops lead added examples of what should fail:

- “ideal for comfortable living”
- “great opportunity”
- “located in a desirable area”

These examples were labeled as generic filler unless tied to concrete facts.

### Improvement

- bland-but-correct descriptions were penalized more consistently

### Remaining issue

- the grader sometimes over-penalized plain listings where only limited detail was available

## Third Refinement: Add Context-Sensitive Specificity Rule

The prompt added:

- judge specificity relative to the richness of available input
- do not fail a draft for lacking details that were never supplied

### Improvement

- false negatives dropped on sparse listings
- reviewers trusted the grader more

## What The Team Learned From Disagreement Analysis

### Pattern 1: Humans cared about misleading implication, not only explicit falsehood

The grader originally missed this. It learned only after the rubric named it clearly.

### Pattern 2: “Technically true” was not enough

For product quality, generic filler is a problem even when the text is factually safe.

### Pattern 3: Grader prompts need their own product owner mindset

The PM treated the grader prompt as an evaluation product, not a utility script. That changed the quality of the refinement process.

## Final Takeaways

### 1. Grader quality comes from rubric clarity

If the rubric is fuzzy, grader disagreement will stay high.

### 2. Negative anchors are powerful

Examples of failure often teach the grader more than examples of success.

### 3. Human disagreement is not an annoyance

It is the raw material for making the grader better.
