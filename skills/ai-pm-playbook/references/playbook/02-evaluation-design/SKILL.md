# Skill: Design An Evaluation System For An AI Agent Or Feature

> **Personalization:** Before starting, paste your completed `my-product/PRODUCT_CONTEXT.md` into the conversation. If you already have an agent or system prompt, include that too. This skill becomes much stronger when it can inspect both the product context and the prompt that defines the agent behavior.

## TL;DR

Use this skill when you need to define how an AI feature or agent will be judged before launch and improved after launch. It helps you turn vague quality goals into a rubric, decide what should be graded by rules, humans, or LLMs, choose the right evaluator implementation, and build a starter CSV dataset with common, edge, and blocker cases.

If you already have an agent prompt, use this skill to bootstrap an eval pack:

- evaluation strategy
- evaluator implementation
- starter rubric dataset in CSV format

## When to Use This

- You are preparing launch criteria for an AI feature or agent
- The team keeps iterating prompts or models without clear proof of improvement
- Stakeholders are asking whether the system is "good enough"
- You need to evaluate a new prompt, model, or routing change against a baseline
- You already have an agent prompt and need a first-pass evaluation strategy
- You want a repeatable way to review AI failures instead of anecdotal discussions

## Prerequisites

- A defined feature or workflow
- At least a rough description of what good output looks like
- Some sample user inputs, outputs, or historical logs if available
- Known high-risk failure types if they already exist
- Optional but high-value: the current agent or system prompt

## Step-by-Step Process

### Step 1: Define The Eval Target From The Workflow Or Prompt

- **What to do:** Start by summarizing what the agent is promising to do. If you have a prompt, extract its explicit and implicit commitments.
- **Key questions to answer:** What job is the agent trying to complete? Which subtasks are in scope? Which tools or actions are implied? What behaviors are forbidden? What failure would violate user trust fastest?
- **Output:** An eval target summary with task boundary, user-facing promises, and blocker failures.
- **Common mistakes:** Jumping into scores before defining what is being judged; trusting the prompt wording without checking what the product actually needs.

### Step 2: Define The Quality Rubric

- **What to do:** Translate "good output" into a small number of explicit dimensions.
- **Key questions to answer:** What makes this output helpful, trustworthy, and usable? Which dimension matters most: relevance, correctness, completeness, tool-use accuracy, tone, structure, safety, or fallback behavior? Which wrong answer would hurt most?
- **Output:** A feature-specific quality rubric.
- **Common mistakes:** Starting with generic scores; mixing user value and internal convenience; omitting agent-specific dimensions like tool choice or state handling.

### Step 3: Choose The Evaluator Architecture

- **What to do:** Decide which parts of the rubric should be owned by rules, an LLM judge, hybrid logic, or humans.
- **Key questions to answer:** Which failures are deterministic? Which quality judgments are interpretive? Which dimensions are too sensitive or fuzzy to automate yet? Should the evaluator be rule-based, LLM-as-judge, hybrid, or human-review-primary?
- **Output:** An evaluator architecture with explicit ownership by dimension.
- **Common mistakes:** Defaulting to LLM-as-judge for everything; using humans for checks that should be deterministic; failing to separate hard blockers from softer quality judgment.

### Step 4: Decide What Needs Rules, Humans, Or Graders

- **What to do:** Separate what can be evaluated deterministically, what needs human review, and what can be graded by an LLM.
- **Key questions to answer:** Which checks are rules-based? Which quality dimensions require interpretation? Which risk areas demand human oversight at least during calibration? Which dimensions can a grader judge reliably?
- **Output:** A scoring plan by signal type.
- **Common mistakes:** Assuming graders can replace humans immediately; asking humans to judge things a rule could judge faster; grading without a clear rubric.

### Step 5: Build The Starter Dataset In CSV Form

- **What to do:** Collect a representative set of examples covering common, edge, adversarial, and blocker cases, then structure them into a CSV that the team can extend.
- **Key questions to answer:** What are the top real-world request types? Which edge cases deserve deliberate coverage? Which blocker failures must appear in the starter set? What should each CSV row capture: user input, prior state, expected behavior, rubric focus, or tool context?
- **Output:** A starter eval dataset in CSV format with clear scenario coverage.
- **Common mistakes:** Sampling only happy-path examples; over-optimizing for quantity before coverage; storing examples in unstructured notes instead of a reusable dataset format.

### Step 6: Draft The Evaluator Implementation

- **What to do:** Implement the evaluator artifact that matches the chosen architecture.
- **Key questions to answer:** If rule-based, what exact checks and error codes are needed? If LLM-as-judge, what context, dimensions, and output schema should the grader receive? If hybrid, which blockers are rules-owned and which dimensions are grader-owned? If human-review-primary, what reviewer rubric and adjudication process are needed?
- **Output:** A rule-based checker spec, grader prompt, hybrid evaluator design, or human review rubric.
- **Common mistakes:** Treating “grader prompt” as the only valid output; leaving aggregation logic vague in hybrid systems; failing to define structured output.

### Step 7: Run Baseline Evaluation

- **What to do:** Score the current system before making large changes so you know what "better" means.
- **Key questions to answer:** What is the current pass rate or rubric score? Which categories fail most? What is the current latency or fallback behavior on the same set? Which blocker failures appear already?
- **Output:** A baseline view of quality and failure patterns.
- **Common mistakes:** Making changes before establishing a baseline; relying only on overall averages.

### Step 8: Calibrate Graders And Analyze Errors

- **What to do:** Calibrate the automated parts of the evaluator against humans, then group failures into categories that imply different fixes.
- **Key questions to answer:** Where do rules miss nuance? Where do graders agree with humans? Where do they drift? Are failures caused by prompt ambiguity, missing grounding, bad routing, poor tool choice, poor data, UI mismatch, or unsupported requests? Which category is most user-harmful?
- **Output:** Evaluator reliability view plus a ranked error taxonomy.
- **Common mistakes:** Trusting automated scores without calibration; treating all failures as one bucket; discussing fixes before categorizing the problem.

### Step 9: Set Launch Gates And Ongoing Review

- **What to do:** Turn the eval results into product decisions.
- **Key questions to answer:** What score or pass threshold is required for launch? Which failure categories are blockers? What gets reviewed daily, weekly, or only after major changes? When do we halt rollout?
- **Output:** Launch gates and an ongoing evaluation cadence.
- **Common mistakes:** Using evals for analysis but not for decision rules; having no rollback threshold.

## Decision Framework

| Eval question | Recommended default |
| --- | --- |
| We only have an agent prompt. Where do we start? | Extract prompt promises, then build a starter eval pack before collecting more logs |
| What should we score first? | Start with the top 3-5 user-facing quality dimensions plus blocker failures |
| How much human review do we need? | More at the start, less once grader reliability is proven |
| How many examples do we need? | Enough to cover common, edge, and high-risk categories before chasing scale |
| What matters more than averages? | Error category distribution, blocker failures, and grader-human disagreement |
| When is the eval "good enough"? | When it can clearly drive launch, rollback, or prioritization decisions |

## Quality Checklist

- [ ] Is the quality rubric specific to the feature or agent?
- [ ] If starting from a prompt, did we translate prompt promises into testable dimensions?
- [ ] Did we explicitly choose the right evaluator type instead of defaulting to LLM-as-judge?
- [ ] Are scoring methods separated into rule-based, human, and grader categories where appropriate?
- [ ] Does the dataset cover common, edge, and high-risk cases?
- [ ] Is there a reusable starter dataset in CSV format?
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

### 3. The Prompt Promise Blind Spot

- **Description:** The agent prompt makes strong claims, but the eval never tests whether those claims are actually kept.
- **Why it happens:** Teams treat the prompt as behavior definition and the eval as a separate task.
- **What to do instead:** Translate prompt promises into rubric dimensions, blocker failures, and dataset slices.

### 4. The Uncalibrated Grader

- **Description:** An LLM grader becomes the truth source without human comparison.
- **Why it happens:** It scales quickly and feels objective.
- **What to do instead:** Measure grader-vs-human agreement and limit grader use where disagreement is high.

### 5. The No-Baseline Problem

- **Description:** Teams compare new versions emotionally because the current system was never scored properly.
- **Why it happens:** Iteration begins before measurement discipline.
- **What to do instead:** Run baseline evals before major prompt or model changes.

### 6. The Analysis Without Gates Pattern

- **Description:** Evals exist, but they do not determine ship/no-ship decisions.
- **Why it happens:** Teams fear over-committing to imperfect numbers.
- **What to do instead:** Define thresholds and blocker categories clearly enough to drive decisions.

## Adaptation Guide

### Tool-Using Agents

Add explicit rubric dimensions for tool choice, parameter correctness, confirmation behavior, and recovery from tool failure.

These agents are usually best served by a hybrid evaluator:

- rules for tool schema, confirmation gates, and action blockers
- grader for grounded explanation, fallback quality, and user-facing clarity

### Structured Output Agents

If the main job is extraction, classification, routing, or constrained formatting, start rule-first.

Add an LLM grader only if there is a meaningful quality dimension that rules cannot judge reliably.

### Multi-Turn Or Stateful Features

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

### High-Risk Workflows

Use stricter blocker definitions and more human oversight, especially on sensitive outputs or external actions.

### High-Volume Consumer Features

Add more coverage for tail behaviors, multilingual variation, and latency-sensitive categories.
