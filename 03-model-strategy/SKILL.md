# Skill: Choose A Model Strategy

> **Context:** In Codex, look for `my-product/PRODUCT_CONTEXT.md` in the current workspace first and use it as the default product context. If local file access is unavailable, ask the user to paste product context manually or use the bundled template.

## TL;DR

Use this skill when you need to decide how a feature should use models, not just which model name to pick. It helps you clarify the task, define the quality bar, choose between prompt-only, bought capability, routing, or custom adaptation, and produce a recommendation that balances quality, latency, cost, and maintainability.

## When to Use This

- You are deciding whether prompt engineering is enough for a feature
- The team is debating build vs. buy vs. custom adaptation
- You need to know if routing is worth the added complexity
- A current feature works, but cost or latency is too high
- Leadership wants a recommendation with clear tradeoffs rather than raw model comparisons

## Prerequisites

- A defined feature or workflow
- Rough quality requirements
- Known latency expectations
- An approximate cost envelope or business sensitivity to spend
- At least some eval or user feedback, if the feature already exists

## Step-by-Step Process

### Step 1: Define The Job The Model Must Do

- **What to do:** Name the exact task, not the model aspiration.
- **Key questions to answer:** Is the model classifying, extracting, generating, routing, summarizing, or reasoning across multiple sources? Which part matters most to the user? Which part is low-risk versus high-risk?
- **Output:** A clear task definition tied to user value.
- **Common mistakes:** Starting with model names; bundling multiple jobs into one vague requirement.

### Step 2: Set The Quality Bar

- **What to do:** Define what good performance actually means for this task.
- **Key questions to answer:** What accuracy, relevance, grounding, or style threshold matters? Which failure type is unacceptable? What quality loss would users actually notice?
- **Output:** A product-relevant quality threshold.
- **Common mistakes:** Using only business KPIs; treating “better” as a direction instead of a threshold.

### Step 3: Set Latency And Cost Boundaries

- **What to do:** Name the acceptable response time and cost sensitivity.
- **Key questions to answer:** Is this real-time, near-real-time, or asynchronous? What cost per task is sustainable? Is the task high enough value to justify a premium path?
- **Output:** Clear operating constraints.
- **Common mistakes:** Discussing model quality in isolation from UX and economics.

### Step 4: Evaluate Simpler Options First

- **What to do:** Ask whether clearer prompts, better context, or improved evals could solve the problem before more complex model strategies.
- **Key questions to answer:** Is the issue actually task definition, context quality, or prompt quality? Have we proven prompt-only is insufficient? What evidence suggests stronger or more specialized modeling is necessary?
- **Output:** A tested baseline path.
- **Common mistakes:** Jumping to fine-tuning or routing because prompt performance is merely “not perfect.”

### Step 5: Choose The Strategic Pattern

- **What to do:** Decide among prompt-only, bought capability, routing, or custom adaptation.
- **Key questions to answer:** Do we need specialization, lower cost at scale, better localization, or more control? Do we have enough data and team capability for custom adaptation? Is routing complexity justified by a real request-tier split?
- **Output:** A recommended model strategy.
- **Common mistakes:** Equating “custom” with “better”; adding routing without measurability.

### Step 6: Define Fallback Logic

- **What to do:** State what happens when the preferred model path is too slow, too expensive, or too weak.
- **Key questions to answer:** When do we escalate to a stronger model? When do we downgrade to a cheaper one? What does the user see when model quality is uncertain? What is the rollback plan?
- **Output:** A fallback chain tied to product rules.
- **Common mistakes:** Treating fallback as only a technical concern.

### Step 7: Produce A Tradeoff Memo

- **What to do:** Summarize the recommendation, rejected alternatives, assumptions, and measurement plan.
- **Key questions to answer:** Why is this the simplest defensible approach? What evidence would change the decision later? How will we know if the strategy is working?
- **Output:** A model strategy recommendation memo.
- **Common mistakes:** Ending with an option list and no point of view.

## Decision Framework

| Situation | Recommended default |
| --- | --- |
| Task is well-bounded and quality is close with prompting | Stay prompt-first |
| Capability exists externally and time-to-ship matters | Buy or integrate before custom building |
| Request difficulty varies a lot | Consider routing with measurement |
| Domain quality requires specialized behavior and enough data exists | Consider custom adaptation carefully |
| Cost is the bottleneck but quality must hold | Route or downgrade low-risk steps first |

## Quality Checklist

- [ ] Is the model task defined clearly and narrowly?
- [ ] Is the quality bar specific enough to measure?
- [ ] Are latency and cost constraints explicit?
- [ ] Have simpler options been evaluated before complex ones?
- [ ] Is the recommended strategy tied to user value, not model hype?
- [ ] Is fallback logic defined?
- [ ] Are routing or custom approaches justified with clear signals?
- [ ] Is there a plan to measure whether the strategy works?

## Anti-Patterns

### 1. The Strongest-Model Default

- **Description:** Use the best available model everywhere.
- **Why it happens:** It feels safest and avoids hard prioritization.
- **What to do instead:** Reserve premium capability for the steps that truly need it.

### 2. The Custom-Build Fantasy

- **Description:** Move toward custom training before proving prompt, context, and eval improvements are exhausted.
- **Why it happens:** Teams want defensibility or differentiation quickly.
- **What to do instead:** Prove the simpler path has plateaued and that the team can support the added burden.

### 3. The Routing Without Evidence Pattern

- **Description:** Introduce model tiers because cost is scary, without proving requests differ meaningfully by difficulty.
- **Why it happens:** Routing sounds efficient in theory.
- **What to do instead:** Define request tiers, expected benefit, and how quality loss will be measured.

### 4. The Vendor-Led Strategy

- **Description:** Product requirements quietly conform to whatever the preferred model vendor is strongest at.
- **Why it happens:** Tool availability drives the conversation.
- **What to do instead:** Hold the product requirement steady first, then choose the model path that fits it.

### 5. The No-Fallback Plan

- **Description:** The chosen model path is treated as the only path.
- **Why it happens:** Teams focus on happy-path demos.
- **What to do instead:** Define downgrade, escalation, or rollback behavior before launch.

## Adaptation Guide

### Early-Stage Teams

Favor prompt-first and integration-first strategies. You need fast learning more than bespoke model ownership.

### High-Volume Consumer Features

Be ruthless about latency and unit economics. Routing and response-length discipline matter more here than in internal tools.

### Regulated Or High-Risk Workflows

Quality and validation matter more than raw cost optimization. Stronger models or tighter fallback paths may be worth the expense.

### Multilingual Products

Test localization quality explicitly. Do not assume a generally strong model performs equally well in your core language or domain style.
