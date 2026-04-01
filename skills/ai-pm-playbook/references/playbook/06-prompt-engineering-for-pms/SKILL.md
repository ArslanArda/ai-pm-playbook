# Skill: Design And Improve Prompts As Product Behavior

> **Context:** In Codex, look for `my-product/PRODUCT_CONTEXT.md` in the current workspace first and use it as the default product context. If local file access is unavailable, ask the user to paste product context manually or use the bundled template.

## TL;DR

Use this skill when you need to define, review, test, or debug prompts for a production AI feature. It helps you frame prompts as behavior specifications, choose the right system-prompt structure, design evaluation and versioning discipline, and diagnose failures systematically instead of tweaking blindly.

## When to Use This

- You are drafting the first production prompt for an AI feature
- Prompt changes are happening informally and causing regressions
- Output quality is unstable and you need a debugging method
- The team needs a prompt review process before launch
- You want PM ownership of behavior without owning implementation details

## Prerequisites

- A defined feature or workflow
- Some clarity on desired behavior and failure risks
- At least sample inputs and outputs if the prompt already exists
- A way to evaluate prompt changes, even if lightweight

## Step-by-Step Process

### Step 1: Define The Behavior

- **What to do:** Describe what the product should do in plain language before writing prompt instructions.
- **Key questions to answer:** What is the assistant’s job? What must it never do? What should happen under ambiguity or low confidence? What output format does the product surface require?
- **Output:** A behavior brief.
- **Common mistakes:** Starting with prompt wording before behavior is clear.

### Step 2: Write The Prompt Structure

- **What to do:** Separate role, constraints, format, examples, and fallback behavior into clear sections.
- **Key questions to answer:** Which instructions are mandatory? Which examples anchor the right behavior? Which constraints must override helpfulness?
- **Output:** A structured prompt draft.
- **Common mistakes:** Mixing priorities into one vague paragraph.

### Step 3: Review Like A Product Spec

- **What to do:** Check whether the prompt expresses the intended product behavior clearly and without contradiction.
- **Key questions to answer:** Could the model reasonably misread this? Are constraints explicit? Is the UI-dependent format fully specified? What happens if context is missing?
- **Output:** A reviewed prompt with known risks noted.
- **Common mistakes:** Reviewing only for tone or clever phrasing.

### Step 4: Version And Test

- **What to do:** Name the prompt version, record what changed, and test against a stable set.
- **Key questions to answer:** What exact behavior changed? Which eval categories should improve? What regressions are plausible?
- **Output:** A versioned prompt change with test evidence.
- **Common mistakes:** Editing prompts in place with no changelog.

### Step 5: Debug Failures Systematically

- **What to do:** Diagnose whether the issue is prompt, model, data, or architecture.
- **Key questions to answer:** Did the prompt instruct the behavior clearly? Did the context include what was needed? Does the failure happen only on one category? Is the model following structure but still lacking capability?
- **Output:** A root-cause hypothesis and fix plan.
- **Common mistakes:** Tweaking wording repeatedly without isolating the problem.

### Step 6: Decide Release Or Rollback

- **What to do:** Use prompt eval results to decide whether the change should ship.
- **Key questions to answer:** Did the change improve the target behavior? Did any high-risk category regress? Is rollback needed? What should be monitored post-release?
- **Output:** A release decision.
- **Common mistakes:** Shipping because the prompt “sounds better” in a few examples.

## Decision Framework

| Symptom | Likely first place to look |
| --- | --- |
| Output ignores important constraints | Prompt clarity or instruction priority |
| Output is well-formed but factually weak | Context or grounding quality |
| Output is inconsistent across similar cases | Prompt ambiguity or model limitation |
| Output format breaks UI | Format instructions or validation gap |
| Quality improved in one area and regressed in another | Prompt tradeoff or conflicting instructions |

## Quality Checklist

- [ ] Is the prompt behavior defined in product terms, not only model terms?
- [ ] Are constraints and refusal conditions explicit?
- [ ] Is the output format fully specified for the UI or downstream consumer?
- [ ] Are examples used deliberately rather than decoratively?
- [ ] Is the prompt versioned with a changelog?
- [ ] Is there an eval plan for prompt changes?
- [ ] Is debugging done by isolating variables?
- [ ] Is rollback possible if the change regresses important categories?

## Anti-Patterns

### 1. The Copy-Tweak Mentality

- **Description:** Prompt changes are treated like minor wording edits.
- **Why it happens:** Prompts look like text, so they feel low-stakes.
- **What to do instead:** Treat them like behavior changes with versioning and review.

### 2. The Prompt Dump

- **Description:** Instructions, examples, and exceptions are all packed into one block.
- **Why it happens:** It feels faster.
- **What to do instead:** Structure prompts by role, rules, format, and examples.

### 3. The Blind Iteration Loop

- **Description:** The team tweaks prompts repeatedly without a hypothesis.
- **Why it happens:** Prompting feels cheap and fast.
- **What to do instead:** State the failure, the expected fix, and the category you want to improve.

### 4. The Hidden Regression

- **Description:** A prompt change helps one case but harms another, and no one notices before launch.
- **Why it happens:** Testing is ad hoc.
- **What to do instead:** Use stable eval coverage and version notes.

### 5. The Prompt-As-Magic Pattern

- **Description:** Teams expect the prompt to overcome missing data, unsupported scope, or weak UX.
- **Why it happens:** Prompt flexibility is seductive.
- **What to do instead:** Fix the actual product boundary when the prompt is being asked to do impossible work.

## Adaptation Guide

### Text Generation

Emphasize groundedness, structure, and style discipline.

### Extraction And Classification

Emphasize schema clarity, ambiguity handling, and low-variance outputs.

### Voice And Conversational Agents

Emphasize brevity, turn-taking, and fallback behavior more heavily.

### Internal Tools

Allow more assistive behavior, but keep review and transparency strong.
