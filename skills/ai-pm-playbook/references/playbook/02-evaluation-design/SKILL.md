# Skill: Design An Evaluation System For An AI Feature

> **Context:** In Codex, look for `my-product/PRODUCT_CONTEXT.md` in the current workspace first and use it as the default product context. If local file access is unavailable, ask the user to paste product context manually or use the bundled template.

## TL;DR

Use this skill when you need to define how an AI feature will be judged before launch and improved after launch. It helps you turn vague quality goals into a rubric, design eval data, choose when to use human review versus graders, analyze errors systematically, and create decision-ready launch gates.

## When to Use This

- You are preparing launch criteria for an AI feature
- The team keeps iterating prompts or models without clear proof of improvement
- Stakeholders are asking whether the system is “good enough”
- You need to evaluate a new prompt, model, or routing change against a baseline
- You want a repeatable way to review AI failures instead of anecdotal discussions

## Prerequisites

- A defined feature or workflow
- At least a rough description of what good output looks like
- Some sample user inputs, outputs, or historical logs
- Known high-risk failure types if they already exist

## Step-by-Step Process

### Step 1: Define The Quality Rubric

- **What to do:** Translate “good output” into a small number of explicit dimensions.
- **Key questions to answer:** What makes this output helpful, trustworthy, and usable? Which dimension matters most: relevance, correctness, completeness, tone, structure, safety? Which wrong answer would hurt most?
- **Output:** A feature-specific quality rubric.
- **Common mistakes:** Starting with generic scores; mixing user value and internal convenience.

### Step 2: Decide What Needs Human Judgment

- **What to do:** Separate what can be evaluated deterministically, what needs human review, and what can be graded by an LLM.
- **Key questions to answer:** Which checks are rules-based? Which quality dimensions require interpretation? Which risk areas demand human oversight at least during calibration?
- **Output:** A scoring plan by signal type.
- **Common mistakes:** Assuming graders can replace humans immediately; asking humans to judge things a rule could judge faster.

### Step 3: Build The Eval Dataset

- **What to do:** Collect a representative set of examples covering common, edge, and adversarial cases.
- **Key questions to answer:** What are the top real-world request types? Which edge cases deserve deliberate coverage? How many examples are enough to reveal meaningful differences for this stage? Which inputs are missing but important?
- **Output:** An initial eval set with scenario coverage.
- **Common mistakes:** Sampling only happy-path examples; over-optimizing for quantity before coverage.

### Step 4: Run Baseline Evaluation

- **What to do:** Score the current system before making large changes so you know what “better” means.
- **Key questions to answer:** What is the current pass rate or rubric score? Which categories fail most? What is the current latency or fallback behavior on the same set?
- **Output:** A baseline view of quality and failure patterns.
- **Common mistakes:** Making changes before establishing a baseline; relying only on overall averages.

### Step 5: Analyze Errors By Category

- **What to do:** Group failures into categories that imply different fixes.
- **Key questions to answer:** Are failures caused by prompt ambiguity, missing grounding, bad routing, poor data, UI mismatch, or unsupported requests? Which category is most user-harmful? Which is most frequent?
- **Output:** A ranked error taxonomy.
- **Common mistakes:** Treating all failures as one bucket; discussing fixes before categorizing the problem.

### Step 6: Calibrate Graders If You Use Them

- **What to do:** Compare grader judgments against human judgments on a representative sample.
- **Key questions to answer:** Where do graders agree with humans? Where do they drift? Do they over-reward polished language? Are they too lenient on subtle hallucinations?
- **Output:** A grader reliability view and usage boundaries.
- **Common mistakes:** Trusting grader scores without calibration; using graders on dimensions they are weak at.

### Step 7: Set Launch Gates And Ongoing Review

- **What to do:** Turn the eval results into product decisions.
- **Key questions to answer:** What score or pass threshold is required for launch? Which failure categories are blockers? What gets reviewed daily, weekly, or only after major changes? When do we halt rollout?
- **Output:** Launch gates and an ongoing evaluation cadence.
- **Common mistakes:** Using evals for analysis but not for decision rules; having no rollback threshold.

## Decision Framework

| Eval question | Recommended default |
| --- | --- |
| What should we score first? | Start with the top 3-5 user-facing quality dimensions |
| How much human review do we need? | More at the start, less once grader reliability is proven |
| How many examples do we need? | Enough to cover common, edge, and high-risk categories before chasing scale |
| What matters more than averages? | Error category distribution and blocker failure types |
| When is the eval “good enough”? | When it can clearly drive launch, rollback, or prioritization decisions |

## Quality Checklist

- [ ] Is the quality rubric specific to the feature?
- [ ] Are scoring methods separated into rule-based, human, and grader categories where appropriate?
- [ ] Does the dataset cover common, edge, and high-risk cases?
- [ ] Is there a baseline before changes are compared?
- [ ] Are failures categorized in a way that suggests different fixes?
- [ ] If graders are used, are they calibrated against humans?
- [ ] Are launch gates explicit?
- [ ] Is there an ongoing review rhythm after launch?

## Anti-Patterns

### 1. The Average Score Trap

- **Description:** The team focuses on a single aggregate score.
- **Why it happens:** It feels easy to communicate.
- **What to do instead:** Track error categories and blocker failures alongside averages.

### 2. The Happy-Path Dataset

- **Description:** The eval set mostly contains easy or common cases.
- **Why it happens:** Those examples are easiest to collect first.
- **What to do instead:** Add explicit edge and adversarial coverage early.

### 3. The Uncalibrated Grader

- **Description:** An LLM grader becomes the truth source without human comparison.
- **Why it happens:** It scales quickly and feels objective.
- **What to do instead:** Measure grader-vs-human agreement and limit grader use where disagreement is high.

### 4. The No-Baseline Problem

- **Description:** Teams compare new versions emotionally because the current system was never scored properly.
- **Why it happens:** Iteration begins before measurement discipline.
- **What to do instead:** Run baseline evals before major prompt or model changes.

### 5. The Analysis Without Gates Pattern

- **Description:** Evals exist, but they do not determine ship/no-ship decisions.
- **Why it happens:** Teams fear over-committing to imperfect numbers.
- **What to do instead:** Define thresholds and blocker categories clearly enough to drive decisions.

## Adaptation Guide

### Early-Stage Features

Bias toward smaller but more thoughtfully curated eval sets and heavier human review.

### Mature Production Systems

Add more automation, richer category tracking, and stronger regression detection across versions.

### High-Risk Workflows

Use stricter blocker definitions and more human oversight, especially on sensitive outputs.

### High-Volume Consumer Features

Add more coverage for tail behaviors, multilingual variation, and latency-sensitive categories.

### Stateful Multi-Turn Features

If the feature updates an existing state rather than responding from scratch, change the basic eval unit.

Instead of evaluating:

- `user input -> output`

evaluate:

- `previous state + new user input -> updated state or updated output`

Examples:

- previous search intent plus new message to updated search intent
- previous agent plan plus user correction to revised plan
- prior draft plus edit instruction to new draft

For these systems, add session-level metrics alongside turn-level metrics:

- context carryover accuracy
- stale context carryover rate
- required context drop rate
- wrong reset or replacement rate
- full-session pass rate across 3-6 turns
